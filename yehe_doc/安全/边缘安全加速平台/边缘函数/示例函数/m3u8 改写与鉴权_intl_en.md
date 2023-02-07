In this example, an m3u8 file is modified by adding authentication information to perform permission control on TS segments.

## Sample Code

```typescript
// A Type-A private key. Specify the required key and make sure that the key remains confidential to prevent leakage.
const pkey = '2ac8ded5-b991-44b1-867c-5ac0f4bb49ee';
// The validity period of the encryption verification key, in seconds.
const expired = 86400 * 7;
// The key name of the URL parameter.
const keyName = 'key';

async function md5Async(text) {
  const hex = (arr) => Array.prototype.map.call(arr, (x) => x >= 16 ? x.toString(16) : '0' + x.toString(16)).join('');
  const arr = await crypto.subtle.digest('MD5', TextEncoder().encode(text));
  return hex(new Uint8Array(arr));
}

// Type-A encoding and verification.
const typeA = {
  encode: async function ({ pkey, pathname, timestamp = Math.floor(Date.now() / 1000), rand = Math.random().toString().replace('0.', ''), uid = 0 }) {
    const src = [pathname, timestamp, rand, uid, pkey].join('-');
    const md5key = await md5Async(src);
    const encodedKey = [timestamp, rand, uid, md5key].join('-');
    return encodedKey;
  },
  check: async function ({ pkey, expired, encodedKey, pathname }) {
    const params = encodedKey.split('-');
    if (params.length !== 4) {
      return false;
    }
    const [timestamp, rand, uid, key] = params;
    const src = [pathname, timestamp, rand, uid, pkey].join('-');
    const md5key = await md5Async(src);
    if (md5key !== key) {
      return false;
    }
    if (Date.now() > (+timestamp + expired) * 1000) {
      return false;
    }
    return true;
  }
};

// Perform Type-A encoding and verification for the URL.
const urlTypeAKey = {
  encode: async function ({ url, pkey, timestamp, rand, uid }) {
    const urlObject = new URL(url);
    const pathname = urlObject.pathname;
    const encodedKey = typeA.encode({ pkey, pathname, timestamp, rand, uid });
    return encodedKey;
  },
  check: async function ({ url, keyName, pkey, expired }) {
    const urlObject = new URL(url);
    const encodedKey = urlObject.searchParams.get(keyName);
    const pathname = urlObject.pathname;
    if (!encodedKey) {
      return false;
    }
    return typeA.check({ pkey, expired, encodedKey, pathname });
  }
}

async function encodeSubUrlTypeAKey(mainUrl, subUrl, { timestamp, rand, uid }) {
  if (/^https?:\/\//.test(subUrl)) {
    return urlTypeAKey.encode({ url: subUrl, pkey, timestamp, rand, uid });
  }
  const urlObject = new URL(mainUrl);
  urlObject.pathname = subUrl[0] === '/' ? subUrl : urlObject.pathname.replace(/\/[^\/]*$/, '/' + subUrl);
  const encodedKey = await urlTypeAKey.encode({ url: urlObject.toString(), pkey, timestamp, rand, uid });
  return encodedKey;
}

// Send a streaming response.
function streamPipe(response) {
  const { readable, writable } = new TransformStream();
  const responseStream = new Response(readable, response);
  response.body.pipeTo(writable);
  responseStream.headers.set('x-pipe-stream', 'true');
  return responseStream;
}

// Add Type-A authentication information for URLs in the m3u8 file.
async function modifyM3u8WithTypeA(response, baseUrl) {
  try {
    const timestamp = Math.floor(Date.now() / 1000);
    const rand = Math.random().toString().replace('0.', '');
    const uid = 0;

    const addKey = async (line) => {
      if (/^\s*$/.test(line)) {
        return line;
      }
      const key = await encodeSubUrlTypeAKey(baseUrl, line, { timestamp, rand, uid });
      if (!key) {
        return line;
      }
      return `${line}?${keyName}=${encodeURIComponent(key)}`;
    }

    const text = await response.text();

    const lines = text.split('\n');
    const trans = lines.map(line => addKey(line));
    const linesNew = await Promise.all(trans);
    const textNew = linesNew.join('\n');

    const responseNew = new Response(textNew, response);
    responseNew.headers.set('x-m3u8-TypeA', 'true');
    return responseNew;
  } catch (e) {
    return new Response(e.toString(), { status: 503 });
  }
}

// Send TS files in streaming mode.
async function fetchTS(request) {
  const response = await fetch(request);
  if (response.status !== 200) {
    return response;
  }

  return streamPipe(response);
}

// Process authentication information about the playback URLs in the m3u8 file.
async function fetchM3u8(request) {
  request.headers.delete('Accept-Encoding');
  const response = await fetch(request);
  if (response.status !== 200) {
    return response;
  }

  return modifyM3u8WithTypeA(response, request.url);
}

// Process the request. The m3u8 file and TS files can be processed.
async function fetchRequest(request) {
  const url = request.url;
  const urlObject = new URL(url);

  if (/.m3u8*$/i.test(urlObject.pathname)) {
    return fetchM3u8(request);
  }

  if (/.ts$/i.test(urlObject.pathname)) {
    return fetchTS(request);
  }

  return new Response(null, { status: 404 });
}

async function handleRequest(request) {
  try {
    const url = request.url;
    const checked = await urlTypeAKey.check({ url, keyName, pkey, expired });
    // Note: If the request does not contain a key, a key is returned. Delete the key in the production environment.
    if (!checked) {
      const data = await urlTypeAKey.encode({ url, pkey });
      return new Response(data, { status: 403 });
    }
    return await fetchRequest(request);
  } catch (e) {
    return new Response(e.stack, { status: 503 });
  }
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
});
```

## Sample Preview

In the address bar of the browser, enter a URL that matches a trigger rule of the edge function to preview the effect of the sample code.

<img src="https://qcloudimg.tencent-cloud.cn/raw/1847f950a58e9b03479273f59f65993d.png" width=609px>

## References
- [Runtime APIs: Fetch](https://www.tencentcloud.com/document/product/1145/52687)
- [Runtime APIs: Web Crypto](https://www.tencentcloud.com/document/product/1145/52693)
- [Runtime APIs: TransformStream](https://www.tencentcloud.com/document/product/1145/52698)
- [Runtime APIs: Response](https://www.tencentcloud.com/document/product/1145/52691)
