This document describes how to use exit codes to troubleshoot pod issues.

## Querying Pod Exceptions
Run the following command to query pod exceptions:
```
kubectl describe pod <pod name>
```
The returned result is as follows:
```bash
Containers:
  kubedns:
    Container ID:  docker://5fb8adf9ee62afc6d3f6f3d9590041818750b392dff015d7091eaaf99cf1c945
    Image:         ccr.ccs.tencentyun.com/library/kubedns-amd64:1.14.4
    Image ID:      docker-pullable://ccr.ccs.tencentyun.com/library/kubedns-amd64@sha256:40790881bbe9ef4ae4ff7fe8b892498eecb7fe6dcc22661402f271e03f7de344
    Ports:         10053/UDP, 10053/TCP, 10055/TCP
    Host Ports:    0/UDP, 0/TCP, 0/TCP
    Args:
      --domain=cluster.local.
      --dns-port=10053
      --config-dir=/kube-dns-config
      --v=2
    State:          Running
      Started:      Tue, 27 Aug 2019 10:58:49 +0800
    Last State:     Terminated
      Reason:       Error
      Exit Code:    255
      Started:      Tue, 27 Aug 2019 10:40:42 +0800
      Finished:     Tue, 27 Aug 2019 10:58:27 +0800
    Ready:          True
    Restart Count:  1
```
`Exit Code` is the status code of the last container exit. If it is not 0, the container exited due to an exception. You can use the exit code to further troubleshoot the problem.

## Exit Codes

* A valid exit code is between 0 and 255.
* 0 means the container exited normally.
* If the container exited due to an external signal, the exit code is between 129 and 255. For example, if the operating system sent `kill -9` or `ctrl+c` as the termination signal, the status is `SIGKILL` or `SIGINT`.
* If the container exited due to an internal signal, the exit code is between 1 and 128. However, in some circumstances, the exit code might be between 129 and 255.
- If the specified exit code has a value outside the 0-255 range, such as `exit(-1)`, it is automatically translated to a value in the 0-255 range.
If the exit code is specified as `code`, it is translated as follows:
    * If the exit code is negative:
```text
256 - (|code| % 256)
```
    * If the exit code is positive:
```text
code % 256
```

## Typical Exit Codes
* **137**: indicates that the process was killed by `SIGKILL`. Possible reasons are:
 * Pod memory reached `resources.limits`, such as Out of Memory (OOM). Pod resource limits are implemented by using Linux cgroup. If the memory of a pod reaches its limit, cgroup forces it to stop (with a similar effect to `kill -9`). If you use `describe pod`, you can see the value of Reason is `OOMKilled`.
 * If the host does not have sufficient resources (OOM), the kernel stops some processes to free up the memory.
>? If the process is stopped due to OOM, cgroup, or the host, you can find relevant records in system logs:
> Ubuntu system logs are stored in `/var/log/syslog`, whereas CentOS system logs are stored in `/var/log/messages`. You can run the `journalctl -k` command to view system logs in both operating systems.
>
 * livenessProbe failed, which causes kubelet to stop the pod.
 * Pod stopped by a trojan process.
* **1** and **255**: indicates common issues. Check container logs for further troubleshooting. For example, this could be the result of `exit(1)` or `exit(-1)`. -1 is translated to 255.



## Standard Linux Interruption Signals

Linux programs send an exit code when they are interrupted by external signals. The value of the exit code is the value of the interrupt signal plus 128. For example, the value of `SIGKILL` is 9, so the program exit code is 9 + 128 = 137. For more standard interrupt signals, see the following table:

<table>
	<tr>
	<th>Signal</th> <th>Status Code Value</th> <th>Action</th> <th>Description</th>
	</tr>
	<tr>
	<td><code>SIGHUP</code></td> <td>1</td> <td>Term</td>
	<td>Hangup detected on controlling terminal or death of controlling process</td>
	</tr>
	<tr>
	<td><code>SIGINT</code></td> <td>2</td> <td>Term</td>
	<td>Interrupt from keyboard</td>
	</tr>
	<tr>
	<td><code>SIGQUIT</code></td> <td>3</td> <td>Core</td>
	<td>Quit from keyboard</td>
	</tr>
	<tr>
	<td><code>SIGILL</code></td> <td>4</td> <td>Core</td>
	<td> Illegal Instruction</td>
	</tr>
	<tr>
	<td><code>SIGABRT</code></td> <td>6</td> <td>Core</td>
	<td>Abort signal from abort(3)</td>
	</tr>
	<tr>
	<td><code>SIGFPE</code></td> <td>8</td> <td>Core</td>
	<td> Floating-point exception</td>
	</tr>
	<tr>
	<td><code>SIGKILL</code></td> <td>9</td> <td>Term</td>
	<td>Kill signal</td>
	</tr>
	<tr>
	<td><code>SIGSEGV</code></td> <td>11</td> <td>Core</td>
	<td>Invalid memory reference</td>
	</tr>
	<tr>
	<td><code>SIGPIPE</code></td> <td>13</td> <td>Term</td>
	<td>Broken pipe: write to pipe with no readers; see pipe(7)</td>
	</tr>
	<tr>
	<td><code>SIGALRM</code></td> <td>14</td> <td>Term</td>
	<td>Timer signal from alarm(2)</td>
	</tr>
	<tr>
	<td><code>SIGTERM</code></td> <td>15</td> <td>Term</td>
	<td>Termination signal</td>
	</tr>
	<tr>
	<td><code>SIGUSR1</code></td> <td>30,10,16 </td> <td>Term</td>
	<td>User-defined signal 1</td>
	</tr>
	<tr>
	<td><code>SIGUSR2</code></td> <td>31,12,17</td> <td>Term</td>
	<td>User-defined signal 2</td>
	</tr>
	<tr>
	<td><code>SIGCHLD</code></td> <td>20,17,18</td> <td>Ign</td>
	<td>Child stopped or terminated</td>
	</tr>
	<tr>
	<td><code>SIGCONT</code></td> <td>19,18,25</td> <td>Cont</td>
	<td> Continue if stopped</td>
	</tr>
	<tr>
	<td><code>SIGSTOP</code></td> <td>17,19,23</td> <td>Stop</td>
	<td>Stop process</td>
	</tr>
	<tr>
	<td><code>SIGTSTP</code></td> <td>18,20,24</td> <td>Stop</td>
	<td>Stop typed at terminal</td>
	</tr>
	<tr>
	<td><code>SIGTTIN</code></td> <td>21,21,26</td> <td>Stop</td>
	<td>Terminal input for background process</td>
	</tr>
	<tr>
	<td><code>SIGTTOU</code></td> <td>22,22,27</td> <td>Stop</td>
	<td>Terminal output for background process</td>
	</tr>
</table>



## C/C++ Exit Codes

`/usr/include/sysexits.h` provides standardized exit codes for C and C++. These codes are described in the following table:

<table>
	<tr>
	<th>Definition</th> <th>Status Code</th> <th>Description</th>
	</tr>
	<tr>
	<td><code>#define EX_OK</code></td> <td>0</td>
	<td>successful termination</td>
	</tr>
	<tr>
	<td><code>#define EX__BASE</code></td> <td>64</td>
	<td>base value for error messages</td>
	</tr>
	<tr>
	<td><code>#define EX_USAGE</code></td> <td>64</td>
	<td>command line usage error</td>
	</tr>
	<tr>
	<td><code>#define EX_DATAERR</code></td> <td>65</td>
	<td>data format error</td>
	</tr>
	<tr>
	<td><code>#define EX_NOINPUT</code></td> <td>66</td>
	<td>cannot open input</td>
	</tr>
	<tr>
	<td><code>#define EX_NOUSER</code></td> <td>67</td>
	<td>addressee unknown</td>
	</tr>
	<tr>
	<td><code>#define EX_NOHOST </code></td> <td>68</td>
	<td> host name unknown</td>
	</tr>
	<tr>
	<td><code>#define EX_UNAVAILABLE</code></td> <td>69</td>
	<td>service unavailable</td>
	</tr>
	<tr>
	<td><code>#define EX_SOFTWARE</code></td> <td>70</td>
	<td>internal software error</td>
	</tr>
	<tr>
	<td><code>#define EX_OSERR </code></td> <td>71</td>
	<td>system error (e.g., can't fork)</td>
	</tr>
	<tr>
	<td><code>#define EX_OSFILE</code></td> <td>72</td>
	<td>critical OS file missing</td>
	</tr>
	<tr>
	<td><code>#define EX_CANTCREAT</code></td> <td>73</td>
	<td>can't create (user) output file</td>
	</tr>
	<tr>
	<td><code>#define EX_IOERR</code></td> <td>74</td>
	<td>input/output error</td>
	</tr>
	<tr>
	<td><code>#define EX_TEMPFAIL</code></td> <td>75</td>
	<td>temp failure; user is invited to retry</td>
	</tr>
	<tr>
	<td><code>#define EX_PROTOCOL</code></td> <td>76</td>
	<td>remote error in protocol</td>
	</tr>
	<tr>
	<td><code>#define EX_NOPERM </code></td> <td>77</td>
	<td>permission denied</td>
	</tr>
	<tr>
	<td><code>#define EX_CONFIG</code></td> <td>78</td>
	<td>configuration error</td>
	</tr>
	<tr>
	<td><code>#define EX__MAX 78</code></td> <td>78</td>
	<td>maximum listed value</td>
		</tr>
</table>



## Status Code Reference

For the description of more status codes, see the following table:
<table>
    <tr>
        <th>Status Code</th>
        <th>Meaning</th>
        <th>Example</th>
        <th>Description</th>
    </tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>Catchall for general errors</td>
<td>let "var1 = 1/0"</td>
<td>Miscellaneous errors, such as <span>"divide by zero"</span> and other impermissible operations</td>
</tr>
<tr>
<td>2</td>
<td>Misuse of shell builtins (according to Bash documentation)</td>
<td>empty_function() {}</td>
<td><a>Missing keyword</a> or command</td>
</tr>
<tr>
 <td>126</td>
<td>Command invoked cannot execute</td>
<td>/dev/null</td>
<td>Permission problem or command is not an executable</td>
</tr>
        <tr>
            <td>127</td>
            <td><span>"command not found"</span></td>
            <td>illegal_command</td>
            <td>Possible problem with <tt>$PATH</tt> or a typo</td>
        </tr>
        <tr>
            <td>128</td>
            <td>Invalid argument to <a> exit</a></td>
            <td>exit 3.14159</td>
            <td><strong>exit</strong> takes only integer args in the range<span>0 - 255</span> (see first footnote)</td>
        </tr>
        <tr>
            <td>128+n</td>
            <td>Fatal error signal <span>"n"</span></td>
            <td><em>kill -9</em> <tt> $PPID</tt> of script</td>
            <td><tt><strong>$?</strong></tt> returns<span>137</span> (128 + 9)</td>
        </tr>
        <tr>
            <td>130</td>
            <td>Script terminated by Control-C</td>
            <td><em>Ctl-C</em></td>
            <td>Control-C is fatal error signal <span> 2</span>, (130 = 128 + 2, see above)</td>
        </tr>
        <tr>
            <td>255*</td>
            <td>Exit status out of range</td>
            <td>exit <span>-1</span></td>
            <td><strong>exit</strong> takes only integer args in the
                range<span>0 - 255</span></td>
        </tr>
    </tbody>
</table>
