## Browsers Supporting DNSPod Certificates Compliant with Chinese Cryptographic Standards
Browsers such as [360](https://browser.360.cn/), [MeSign](https://www.mesince.com/zh-cn/browser), and Haitai support Chinese cryptographic algorithms.

## Browser Compatibility of DNSPod Certificates Compliant with Chinese Cryptographic Standards
Sites using SSL certificates adopting Chinese cryptographic algorithms can be accessed through Chinese cryptographic browsers. However, since Chinese cryptographic algorithms are not compatible with all mainstream browsers, certain mainstream browsers that support only international cryptographic algorithms will report errors for SSL certificates using Chinese cryptographic algorithms. 
A solution to this problem is dual certificate deployment and adaptive browser compatibility. With this solution, both browsers supporting Chinese cryptographic algorithms and those supporting only international cryptographic algorithms are supported, and you can visit websites through any browser. This solution meets the compliance requirements of deploying SSL certificates using Chinese cryptographic algorithms and the availability, usability, and global versatility requirements of websites, and tackles the technical barriers for the application of SSL certificates using Chinese cryptographic algorithms.  

## Browser Differences Among Different Types of DNSPod Certificates Compliant with Chinese Cryptographic Standards

<table>
<thead>
  <tr>
    <th>Certificate Type</th>
    <th>OV</th>
    <th>DV</th>
    <th>EV</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Supporting wildcard domain names</td>
    <td>Supported</td>
    <td>Supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td>Supporting multiple domain names</td>
    <td colspan="3">Supported (up to 100 domain names)</td>
  </tr>
  <tr>
    <td>Cryptographic algorithms</td>
    <td colspan="3">Adopting the Chinese cryptographic algorithm system SM2 to deliver better key strength than international cryptographic standards</td>
  </tr>
  <tr>
    <td>Browser compatibility</td>
    <td colspan="3">Compatible with browsers supporting Chinese cryptographic algorithms, such as 360, MeSign, and Haitai</td>
  </tr>
</tbody>
</table>

**Address bar differences for DNSPod certificates compliant with Chinese cryptographic standards**
- DV: displays the security lock icon in browsers supporting Chinese cryptographic algorithms.
- OV: displays the security lock icon and the organization name in browsers supporting Chinese cryptographic algorithms.
- EV: displays the green address bar and the organization name in browsers supporting Chinese cryptographic algorithms.









