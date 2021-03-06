# 操作系统 (OS)

<!--introduced_in=v0.10.0-->

> 稳定性：2 - 稳定

The `os` module provides operating system-related utility methods and properties. 可以通过如下方式访问：

```js
const os = require('os');
```

## `os.EOL`
<!-- YAML
added: v0.7.8
-->

* {string}

The operating system-specific end-of-line marker.

* `\n` 在 POSIX 系统上
* `\r\n` 在 Windows 系统上

## `os.arch()`
<!-- YAML
added: v0.5.0
-->

* 返回：{string}

Returns the operating system CPU architecture for which the Node.js binary was compiled. Possible values are `'arm'`, `'arm64'`, `'ia32'`, `'mips'`, `'mipsel'`, `'ppc'`, `'ppc64'`, `'s390'`, `'s390x'`, `'x32'`, and `'x64'`.

The return value is equivalent to [`process.arch`][].

## `os.constants`
<!-- YAML
added: v6.3.0
-->

* {Object}

Contains commonly used operating system-specific constants for error codes, process signals, and so on. The specific constants defined are described in [OS Constants](#os_os_constants_1).

## `os.cpus()`
<!-- YAML
added: v0.3.3
-->

* 返回: {Object[]}

Returns an array of objects containing information about each logical CPU core.

在每个对象中包含的属性包括：

* `model` {string}
* `speed` {number} (以 MHz 为单位)
* `times` {Object}
  * `user` {number} 在用户模式下使用的 CPU 毫秒数。
  * `nice` {number} 在良好模式下使用的 CPU 毫秒数。
  * `sys` {number} 在系统模式下使用的 CPU 毫秒数。
  * `idle` {number} 在空闲模式下使用的 CPU 毫秒数。
  * `irq` {number} 在中断模式下使用的 CPU 毫秒数。
```js
[
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 252020,
      nice: 0,
      sys: 30340,
      idle: 1070356870,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 306960,
      nice: 0,
      sys: 26980,
      idle: 1071569080,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 248450,
      nice: 0,
      sys: 21750,
      idle: 1070919370,
      irq: 0
    }
  },
  {
    model: 'Intel(R) Core(TM) i7 CPU         860  @ 2.80GHz',
    speed: 2926,
    times: {
      user: 256880,
      nice: 0,
      sys: 19430,
      idle: 1070905480,
      irq: 20
    }
  }
]
```

`nice` values are POSIX-only. On Windows, the `nice` values of all processors are always 0.

## `os.endianness()`<!-- YAML
added: v0.9.4
-->* 返回：{string}

Returns a string identifying the endianness of the CPU for which the Node.js binary was compiled.

Possible values are `'BE'` for big endian and `'LE'` for little endian.

## `os.freemem()`<!-- YAML
added: v0.3.3
-->* 返回：{integer}

Returns the amount of free system memory in bytes as an integer.

## `os.getPriority([pid])`<!-- YAML
added: v10.10.0
-->* `pid` {integer} The process ID to retrieve scheduling priority for. **Default** `0`.
* 返回：{integer}

Returns the scheduling priority for the process specified by `pid`. If `pid` is not provided or is `0`, the priority of the current process is returned.

## `os.homedir()`<!-- YAML
added: v2.3.0
-->* 返回：{string}

Returns the string path of the current user's home directory.

On POSIX, it uses the `$HOME` environment variable if defined. Otherwise it uses the [effective UID](https://en.wikipedia.org/wiki/User_identifier#Effective_user_ID) to look up the user's home directory.

On Windows, it uses the `USERPROFILE` environment variable if defined. Otherwise it uses the path to the profile directory of the current user.

## `os.hostname()`<!-- YAML
added: v0.3.3
-->* 返回：{string}

Returns the hostname of the operating system as a string.

## `os.loadavg()`
<!-- YAML
added: v0.3.3
-->

* Returns: {number[]}

Returns an array containing the 1, 5, and 15 minute load averages.

The load average is a measure of system activity calculated by the operating system and expressed as a fractional number.

The load average is a Unix-specific concept. On Windows, the return value is always `[0, 0, 0]`.

## `os.networkInterfaces()`<!-- YAML
added: v0.6.0
-->* 返回：{Object}

Returns an object containing network interfaces that have been assigned a network address.

在返回对象中，每个键值标识了一个网络接口。 相关的值是一个对象数组，其中每个对象描述一个被分配的网址。

被赋予网络地址的对象包含的属性包括：

* `address` {string} 被赋予的 IPv4 或 IPv6 地址
* `netmask` {string} IPv4 或 IPv6 网络掩码
* `family` {string} `IPv4` 或 `IPv6`
* `mac` {string} 网络接口的 MAC 地址
* `internal` {boolean} 当网络接口为 loopback 或相似的不能远程访问的接口时，其值为 `true`，否则其值为 `false`
* `scopeid` {number} 数字型的 IPv6 域 ID (只有当 `family` 为`IPv6` 时需要指定)
* `cidr` {string} The assigned IPv4 or IPv6 address with the routing prefix in CIDR notation. If the `netmask` is invalid, this property is set to `null`.
```js
{
  lo: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      scopeid: 0,
      internal: true,
      cidr: '::1/128'
    }
  ],
  eth0: [
    {
      address: '192.168.1.108',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: '01:02:03:0a:0b:0c',
      internal: false,
      cidr: '192.168.1.108/24'
    },
    {
      address: 'fe80::a00:27ff:fe4e:66a1',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: '01:02:03:0a:0b:0c',
      scopeid: 1,
      internal: false,
      cidr: 'fe80::a00:27ff:fe4e:66a1/64'
    }
  ]
}
```

## `os.platform()`<!-- YAML
added: v0.5.0
-->* 返回：{string}

Returns a string identifying the operating system platform. The value is set at compile time. Possible values are `'aix'`, `'darwin'`, `'freebsd'`, `'linux'`, `'openbsd'`, `'sunos'`, and `'win32'`.

The return value is equivalent to [`process.platform`][].

The value `'android'` may also be returned if Node.js is built on the Android operating system. [Android support is experimental](https://github.com/nodejs/node/blob/master/BUILDING.md#androidandroid-based-devices-eg-firefox-os).

## `os.release()`<!-- YAML
added: v0.3.3
-->* 返回：{string}

Returns the operating system as a string.

On POSIX systems, the operating system release is determined by calling [uname(3)](https://linux.die.net/man/3/uname). 在 Windows 系统上，使用 `GetVersionExW()`。 See https://en.wikipedia.org/wiki/Uname#Examples for more information.

## `os.setPriority([pid, ]priority)`<!-- YAML
added: v10.10.0
-->* `pid` {integer} The process ID to set scheduling priority for. **Default** `0`.
* `priority` {integer} The scheduling priority to assign to the process.

Attempts to set the scheduling priority for the process specified by `pid`. If `pid` is not provided or is `0`, the process ID of the current process is used.

The `priority` input must be an integer between `-20` (high priority) and `19` (low priority). Due to differences between Unix priority levels and Windows priority classes, `priority` is mapped to one of six priority constants in `os.constants.priority`. When retrieving a process priority level, this range mapping may cause the return value to be slightly different on Windows. To avoid confusion, set `priority` to one of the priority constants.

On Windows, setting priority to `PRIORITY_HIGHEST` requires elevated user privileges. Otherwise the set priority will be silently reduced to `PRIORITY_HIGH`.

## `os.tmpdir()`<!-- YAML
added: v0.9.9
changes:
  - version: v2.0.0
    pr-url: https://github.com/nodejs/node/pull/747
    description: This function is now cross-platform consistent and no longer
                 returns a path with a trailing slash on any platform
-->* 返回：{string}

Returns the operating system's default directory for temporary files as a string.

## `os.totalmem()`<!-- YAML
added: v0.3.3
-->* 返回：{integer}

Returns the total amount of system memory in bytes as an integer.

## `os.type()`<!-- YAML
added: v0.3.3
-->* 返回：{string}

Returns the operating system name as returned by [uname(3)](https://linux.die.net/man/3/uname). For example, it returns `'Linux'` on Linux, `'Darwin'` on macOS, and `'Windows_NT'` on Windows.

See https://en.wikipedia.org/wiki/Uname#Examples for additional information about the output of running [uname(3)](https://linux.die.net/man/3/uname) on various operating systems.

## `os.uptime()`<!-- YAML
added: v0.3.3
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/20129
    description: The result of this function no longer contains a fraction
                 component on Windows.
-->* 返回：{integer}

Returns the system uptime in number of seconds.

## `os.userInfo([options])`<!-- YAML
added: v6.0.0
-->* `options` {Object}
  * `encoding` {string} 用于解释结果字符串的字符编码。 如果 `encoding` 被设置为 `'buffer'`，则 `username`, `shell`, 和 `homedir` 将会是 `Buffer` 的实例。 **Default:** `'utf8'`.
* 返回：{Object}

Returns information about the currently effective user. On POSIX platforms, this is typically a subset of the password file. The returned object includes the `username`, `uid`, `gid`, `shell`, and `homedir`. On Windows, the `uid` and `gid` fields are `-1`, and `shell` is `null`.

`os.userInfo()` 返回的 `homedir` 值由操作系统提供。 This differs from the result of `os.homedir()`, which queries environment variables for the home directory before falling back to the operating system response.

Throws a [`SystemError`][] if a user has no `username` or `homedir`.

## 操作系统常量

`os.constants` 会导出如下常量。

Not all constants will be available on every operating system.

### 信号常量<!-- YAML
changes:
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6093
    description: Added support for `SIGINFO`.
-->The following signal constants are exported by `os.constants.signals`.

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>SIGHUP</code></td>
    <td>发送此信号来表明一个控制终端关闭或者是父进程退出。</td>
  </tr>
  <tr>
    <td><code>SIGINT</code></td>
    <td>Sent to indicate when a user wishes to interrupt a process
    (<code>(Ctrl+C)</code>).</td>
  </tr>
  <tr>
    <td><code>SIGQUIT</code></td>
    <td>发送此信号来表明用户希望终止进程并执行核心转储。</td>
  </tr>
  <tr>
    <td><code>SIGILL</code></td>
    <td>发送此信号给一个进程来通知该进程试图运行一个非法的，异常的，未知的，或特权的指令。</td>
  </tr>
  <tr>
    <td><code>SIGTRAP</code></td>
    <td>当发生异常时，发送此信号给一个进程。</td>
  </tr>
  <tr>
    <td><code>SIGABRT</code></td>
    <td>发送此信号给一个进程来请求终止。</td>
  </tr>
  <tr>
    <td><code>SIGIOT</code></td>
    <td><code>SIGABRT</code> 的同义词</td>
  </tr>
  <tr>
    <td><code>SIGBUS</code></td>
    <td>发送此信号给一个进程来通知该进程已经造成了总线错误。</td>
  </tr>
  <tr>
    <td><code>SIGFPE</code></td>
    <td>发送此信号给一个进程来通知该进程进行了一个非法的算术操作。</td>
  </tr>
  <tr>
    <td><code>SIGKILL</code></td>
    <td>发送此信号给一个进程来立即终止该进程。</td>
  </tr>
  <tr>
    <td><code>SIGUSR1</code> <code>SIGUSR2</code></td>
    <td>发送此信号给一个进程来识别用户定义的条件。</td>
  </tr>
  <tr>
    <td><code>SIGSEGV</code></td>
    <td>发送此信号给一个进程来通知段错误。</td>
  </tr>
  <tr>
    <td><code>SIGPIPE</code></td>
    <td>当进程试图向已断开连接的管道写入时发送此信号给该进程。</td>
  </tr>
  <tr>
    <td><code>SIGALRM</code></td>
    <td>当系统定时器到点时，发送此信号到进程。</td>
  </tr>
  <tr>
    <td><code>SIGTERM</code></td>
    <td>发送此信号给一个进程来请求终止。</td>
  </tr>
  <tr>
    <td><code>SIGCHLD</code></td>
    <td>当子进程终止时发送此信号给其父进程。</td>
  </tr>
  <tr>
    <td><code>SIGSTKFLT</code></td>
    <td>发送此信号给一个进程来表明一个协处理器的栈错误。</td>
  </tr>
  <tr>
    <td><code>SIGCONT</code></td>
    <td>发送此信号来指示操作系统继续一个暂停的进程。</td>
  </tr>
  <tr>
    <td><code>SIGSTOP</code></td>
    <td>发送此信号来指示操作系统停止一个进程。</td>
  </tr>
  <tr>
    <td><code>SIGTSTP</code></td>
    <td>发送此信号来请求停止一个进程。</td>
  </tr>
  <tr>
    <td><code>SIGBREAK</code></td>
    <td>当用户希望终止一个进程时，发送此信号。</td>
  </tr>
  <tr>
    <td><code>SIGTTIN</code></td>
    <td>当进程在后台读取 TTY 时，发送此信号给该进程。</td>
  </tr>
  <tr>
    <td><code>SIGTTOU</code></td>
    <td>当进程在后台写入到 TTY 时，发送此信号给该进程。</td>
  </tr>
  <tr>
    <td><code>SIGURG</code></td>
    <td>当套接字有紧急的数据需要读取时，发送此信号给进程。</td>
  </tr>
  <tr>
    <td><code>SIGXCPU</code></td>
    <td>当进程超过其在 CPU 上的使用限制时，发送此信号给该进程。</td>
  </tr>
  <tr>
    <td><code>SIGXFSZ</code></td>
    <td>当进程生成的文件大小超过最大允许值时，发送此信号给该进程。</td>
  </tr>
  <tr>
    <td><code>SIGVTALRM</code></td>
    <td>当虚拟定时器到点时，发送此信号到进程。</td>
  </tr>
  <tr>
    <td><code>SIGPROF</code></td>
    <td>当系统定时器到点时，发送此信号到进程。</td>
  </tr>
  <tr>
    <td><code>SIGWINCH</code></td>
    <td>当控制终端改变大小时，发送此信号到进程。</td>
  </tr>
  <tr>
    <td><code>SIGIO</code></td>
    <td>当 I/O 可用时，发送此信号到进程。</td>
  </tr>
  <tr>
    <td><code>SIGPOLL</code></td>
    <td><code>SIGIO</code> 的同义词</td>
  </tr>
  <tr>
    <td><code>SIGLOST</code></td>
    <td>当文件锁丢失时发送此信号给进程。</td>
  </tr>
  <tr>
    <td><code>SIGPWR</code></td>
    <td>发送此信号给一个进程来通知电源故障。</td>
  </tr>
  <tr>
    <td><code>SIGINFO</code></td>
    <td><code>SIGPWR</code> 的同义词</td>
  </tr>
  <tr>
    <td><code>SIGSYS</code></td>
    <td>发送此信号给一个进程来通知参数错误。</td>
  </tr>
  <tr>
    <td><code>SIGUNUSED</code></td>
    <td><code>SIGSYS</code> 的同义词</td>
  </tr>
</table>

### 错误常量

The following error constants are exported by `os.constants.errno`.

#### POSIX 错误常量

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>E2BIG</code></td>
    <td>表明参数列表比预期的要长。</td>
  </tr>
  <tr>
    <td><code>EACCES</code></td>
    <td>表明操作没有足够的权限。</td>
  </tr>
  <tr>
    <td><code>EADDRINUSE</code></td>
    <td>表明网络地址已经被使用。</td>
  </tr>
  <tr>
    <td><code>EADDRNOTAVAIL</code></td>
    <td>表明网络地址当前不可用。</td>
  </tr>
  <tr>
    <td><code>EAFNOSUPPORT</code></td>
    <td>表明不支持的网络地址系列。</td>
  </tr>
  <tr>
    <td><code>EAGAIN</code></td>
    <td>Indicates that there is no data available and to try the
    operation again later.</td>
  </tr>
  <tr>
    <td><code>EALREADY</code></td>
    <td>表明套接字已经有正在进行的连接。</td>
  </tr>
  <tr>
    <td><code>EBADF</code></td>
    <td>表明文件描述符无效。</td>
  </tr>
  <tr>
    <td><code>EBADMSG</code></td>
    <td>表明无效的数据消息。</td>
  </tr>
  <tr>
    <td><code>EBUSY</code></td>
    <td>表明设备或资源忙碌中。</td>
  </tr>
  <tr>
    <td><code>ECANCELED</code></td>
    <td>表明一个操作已经被取消。</td>
  </tr>
  <tr>
    <td><code>ECHILD</code></td>
    <td>表明没有子进程。</td>
  </tr>
  <tr>
    <td><code>ECONNABORTED</code></td>
    <td>表明网络连接被中断。</td>
  </tr>
  <tr>
    <td><code>ECONNREFUSED</code></td>
    <td>表明网络连接被拒绝。</td>
  </tr>
  <tr>
    <td><code>ECONNRESET</code></td>
    <td>表明网络连接被重置。</td>
  </tr>
  <tr>
    <td><code>EDEADLK</code></td>
    <td>表明已避免了一个资源死锁。</td>
  </tr>
  <tr>
    <td><code>EDESTADDRREQ</code></td>
    <td>表明需要一个目标地址。</td>
  </tr>
  <tr>
    <td><code>EDOM</code></td>
    <td>表明参数超出了函数作用域。</td>
  </tr>
  <tr>
    <td><code>EDQUOT</code></td>
    <td>表明超出了磁盘限额。</td>
  </tr>
  <tr>
    <td><code>EEXIST</code></td>
    <td>表明文件已经存在。</td>
  </tr>
  <tr>
    <td><code>EFAULT</code></td>
    <td>表明一个无效的指针地址。</td>
  </tr>
  <tr>
    <td><code>EFBIG</code></td>
    <td>表明文件太大了。</td>
  </tr>
  <tr>
    <td><code>EHOSTUNREACH</code></td>
    <td>表明主机无法访问。</td>
  </tr>
  <tr>
    <td><code>EIDRM</code></td>
    <td>表明已删除标识符。</td>
  </tr>
  <tr>
    <td><code>EILSEQ</code></td>
    <td>表明无效的字节序列。</td>
  </tr>
  <tr>
    <td><code>EINPROGRESS</code></td>
    <td>表明操作正在进行中。</td>
  </tr>
  <tr>
    <td><code>EINTR</code></td>
    <td>表明一个函数调用被中断。</td>
  </tr>
  <tr>
    <td><code>EINVAL</code></td>
    <td>表明提供了无效参数。</td>
  </tr>
  <tr>
    <td><code>EIO</code></td>
    <td>表明其他的，不确定的 I/O 错误。</td>
  </tr>
  <tr>
    <td><code>EISCONN</code></td>
    <td>表明套接字已连接。</td>
  </tr>
  <tr>
    <td><code>EISDIR</code></td>
    <td>表明路径为一个目录。</td>
  </tr>
  <tr>
    <td><code>ELOOP</code></td>
    <td>表明路径中有太多层的符号连接。</td>
  </tr>
  <tr>
    <td><code>EMFILE</code></td>
    <td>表明打开了太多的文件。</td>
  </tr>
  <tr>
    <td><code>EMLINK</code></td>
    <td>表明文件上有太多的硬连接。</td>
  </tr>
  <tr>
    <td><code>EMSGSIZE</code></td>
    <td>表明提供的消息太长了。</td>
  </tr>
  <tr>
    <td><code>EMULTIHOP</code></td>
    <td>表明尝试了多跳。</td>
  </tr>
  <tr>
    <td><code>ENAMETOOLONG</code></td>
    <td>表明文件名过长。</td>
  </tr>
  <tr>
    <td><code>ENETDOWN</code></td>
    <td>表明网络关闭。</td>
  </tr>
  <tr>
    <td><code>ENETRESET</code></td>
    <td>表明连接被网络终止。</td>
  </tr>
  <tr>
    <td><code>ENETUNREACH</code></td>
    <td>表明网络不可用。</td>
  </tr>
  <tr>
    <td><code>ENFILE</code></td>
    <td>表明在系统中打开的文件过多。</td>
  </tr>
  <tr>
    <td><code>ENOBUFS</code></td>
    <td>表明没有可用的缓冲区空间。</td>
  </tr>
  <tr>
    <td><code>ENODATA</code></td>
    <td>表明在流头部读取队列中没有可用的消息。</td>
  </tr>
  <tr>
    <td><code>ENODEV</code></td>
    <td>表明没有此设备。</td>
  </tr>
  <tr>
    <td><code>ENOENT</code></td>
    <td>表明没有此文件或目录。</td>
  </tr>
  <tr>
    <td><code>ENOEXEC</code></td>
    <td>表明一个执行格式错误。</td>
  </tr>
  <tr>
    <td><code>ENOLCK</code></td>
    <td>表明没有可用的锁。</td>
  </tr>
  <tr>
    <td><code>ENOLINK</code></td>
    <td>表明链接已被切断。</td>
  </tr>
  <tr>
    <td><code>ENOMEM</code></td>
    <td>表明没有足够的空间。</td>
  </tr>
  <tr>
    <td><code>ENOMSG</code></td>
    <td>表明没有期待类型的消息。</td>
  </tr>
  <tr>
    <td><code>ENOPROTOOPT</code></td>
    <td>表明给定的协议不可用。</td>
  </tr>
  <tr>
    <td><code>ENOSPC</code></td>
    <td>表明在此设备上没有可用空间。</td>
  </tr>
  <tr>
    <td><code>ENOSR</code></td>
    <td>表明没有流资源可用。</td>
  </tr>
  <tr>
    <td><code>ENOSTR</code></td>
    <td>表明给定的资源不是流。</td>
  </tr>
  <tr>
    <td><code>ENOSYS</code></td>
    <td>表明函数尚未被实现。</td>
  </tr>
  <tr>
    <td><code>ENOTCONN</code></td>
    <td>表明套接字未被连接。</td>
  </tr>
  <tr>
    <td><code>ENOTDIR</code></td>
    <td>表明路径不是一个目录。</td>
  </tr>
  <tr>
    <td><code>ENOTEMPTY</code></td>
    <td>表明目录非空。</td>
  </tr>
  <tr>
    <td><code>ENOTSOCK</code></td>
    <td>表明给定的项目不是套接字。</td>
  </tr>
  <tr>
    <td><code>ENOTSUP</code></td>
    <td>表明给定的操作不被支持。</td>
  </tr>
  <tr>
    <td><code>ENOTTY</code></td>
    <td>表明不恰当的 I/O 控制操作。</td>
  </tr>
  <tr>
    <td><code>ENXIO</code></td>
    <td>表明没有此设备或地址。</td>
  </tr>
  <tr>
    <td><code>EOPNOTSUPP</code></td>
    <td>表明在套接字上不支持的操作。 Although
    <code>ENOTSUP</code> and <code>EOPNOTSUPP</code> have the same value
    on Linux, according to POSIX.1 these error values should be distinct.)</td>
  </tr>
  <tr>
    <td><code>EOVERFLOW</code></td>
    <td>表明值过长以至于不能存储到给定的数据类型中。</td>
  </tr>
  <tr>
    <td><code>EPERM</code></td>
    <td>表明操作不被允许。</td>
  </tr>
  <tr>
    <td><code>EPIPE</code></td>
    <td>表明一个断开的管道。</td>
  </tr>
  <tr>
    <td><code>EPROTO</code></td>
    <td>表明一个协议错误。</td>
  </tr>
  <tr>
    <td><code>EPROTONOSUPPORT</code></td>
    <td>表明一个不支持的协议。</td>
  </tr>
  <tr>
    <td><code>EPROTOTYPE</code></td>
    <td>表明套接字协议类型错误。</td>
  </tr>
  <tr>
    <td><code>ERANGE</code></td>
    <td>表明结果太大了。</td>
  </tr>
  <tr>
    <td><code>EROFS</code></td>
    <td>表明文件系统为只读。</td>
  </tr>
  <tr>
    <td><code>ESPIPE</code></td>
    <td>表明无效的搜索操作。</td>
  </tr>
  <tr>
    <td><code>ESRCH</code></td>
    <td>表明没有此进程。</td>
  </tr>
  <tr>
    <td><code>ESTALE</code></td>
    <td>表明文件句柄是旧的。</td>
  </tr>
  <tr>
    <td><code>ETIME</code></td>
    <td>表明已过期的定时器。</td>
  </tr>
  <tr>
    <td><code>ETIMEDOUT</code></td>
    <td>表明连接超时。</td>
  </tr>
  <tr>
    <td><code>ETXTBSY</code></td>
    <td>表明文本文件忙。</td>
  </tr>
  <tr>
    <td><code>EWOULDBLOCK</code></td>
    <td>表明此操作会阻塞。</td>
  </tr>
  <tr>
    <td><code>EXDEV</code></td>
    <td>表明一个不正确的链接。
  </tr>
</table>

#### Windows 系统特定的错误常量。

The following error codes are specific to the Windows operating system.

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>WSAEINTR</code></td>
    <td>表明被终止的函数调用。</td>
  </tr>
  <tr>
    <td><code>WSAEBADF</code></td>
    <td>表明无效的文件句柄。</td>
  </tr>
  <tr>
    <td><code>WSAEACCES</code></td>
    <td>表明权限不足以完成此操作。</td>
  </tr>
  <tr>
    <td><code>WSAEFAULT</code></td>
    <td>表明一个无效的指针地址。</td>
  </tr>
  <tr>
    <td><code>WSAEINVAL</code></td>
    <td>表明传递了无效的参数。</td>
  </tr>
  <tr>
    <td><code>WSAEMFILE</code></td>
    <td>表明打开了太多的文件。</td>
  </tr>
  <tr>
    <td><code>WSAEWOULDBLOCK</code></td>
    <td>表明资源暂时不可用。</td>
  </tr>
  <tr>
    <td><code>WSAEINPROGRESS</code></td>
    <td>表明操作正在进行中。</td>
  </tr>
  <tr>
    <td><code>WSAEALREADY</code></td>
    <td>表明操作正在进行中。</td>
  </tr>
  <tr>
    <td><code>WSAENOTSOCK</code></td>
    <td>表明资源不是套接字。</td>
  </tr>
  <tr>
    <td><code>WSAEDESTADDRREQ</code></td>
    <td>表明需要一个目标地址。</td>
  </tr>
  <tr>
    <td><code>WSAEMSGSIZE</code></td>
    <td>表明消息尺寸太长。</td>
  </tr>
  <tr>
    <td><code>WSAEPROTOTYPE</code></td>
    <td>表明套接字的协议类型错误。</td>
  </tr>
  <tr>
    <td><code>WSAENOPROTOOPT</code></td>
    <td>表明错误的协议选项。</td>
  </tr>
  <tr>
    <td><code>WSAEPROTONOSUPPORT</code></td>
    <td>表明不支持的协议。</td>
  </tr>
  <tr>
    <td><code>WSAESOCKTNOSUPPORT</code></td>
    <td>表明不支持的套接字类型。</td>
  </tr>
  <tr>
    <td><code>WSAEOPNOTSUPP</code></td>
    <td>表明不支持的操作。</td>
  </tr>
  <tr>
    <td><code>WSAEPFNOSUPPORT</code></td>
    <td>表明不支持的协议系列。</td>
  </tr>
  <tr>
    <td><code>WSAEAFNOSUPPORT</code></td>
    <td>表明不支持的地址系列。</td>
  </tr>
  <tr>
    <td><code>WSAEADDRINUSE</code></td>
    <td>表明网络地址已经被使用。</td>
  </tr>
  <tr>
    <td><code>WSAEADDRNOTAVAIL</code></td>
    <td>表明网络地址不可用。</td>
  </tr>
  <tr>
    <td><code>WSAENETDOWN</code></td>
    <td>表明网络关闭。</td>
  </tr>
  <tr>
    <td><code>WSAENETUNREACH</code></td>
    <td>表明网络不可用。</td>
  </tr>
  <tr>
    <td><code>WSAENETRESET</code></td>
    <td>表明网络连接被重置。</td>
  </tr>
  <tr>
    <td><code>WSAECONNABORTED</code></td>
    <td>表明连接已被中断。</td>
  </tr>
  <tr>
    <td><code>WSAECONNRESET</code></td>
    <td>表明连接已被对等方重置。</td>
  </tr>
  <tr>
    <td><code>WSAENOBUFS</code></td>
    <td>表明没有可用的缓冲区空间。</td>
  </tr>
  <tr>
    <td><code>WSAEISCONN</code></td>
    <td>表明套接字已连接。</td>
  </tr>
  <tr>
    <td><code>WSAENOTCONN</code></td>
    <td>表明套接字未被连接。</td>
  </tr>
  <tr>
    <td><code>WSAESHUTDOWN</code></td>
    <td>表明在套接字关闭后不能发送数据。</td>
  </tr>
  <tr>
    <td><code>WSAETOOMANYREFS</code></td>
    <td>表明有太多的引用。</td>
  </tr>
  <tr>
    <td><code>WSAETIMEDOUT</code></td>
    <td>表明连接超时。</td>
  </tr>
  <tr>
    <td><code>WSAECONNREFUSED</code></td>
    <td>表明连接已被拒绝。</td>
  </tr>
  <tr>
    <td><code>WSAELOOP</code></td>
    <td>表明名称不能被翻译。</td>
  </tr>
  <tr>
    <td><code>WSAENAMETOOLONG</code></td>
    <td>表明名称过长。</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTDOWN</code></td>
    <td>表明网络主机已关闭。</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTUNREACH</code></td>
    <td>表明没有到网络主机的路由。</td>
  </tr>
  <tr>
    <td><code>WSAENOTEMPTY</code></td>
    <td>表明目录非空。</td>
  </tr>
  <tr>
    <td><code>WSAEPROCLIM</code></td>
    <td>表明有太多进程。</td>
  </tr>
  <tr>
    <td><code>WSAEUSERS</code></td>
    <td>表明已超过用户限额。</td>
  </tr>
  <tr>
    <td><code>WSAEDQUOT</code></td>
    <td>表明超出了磁盘限额。</td>
  </tr>
  <tr>
    <td><code>WSAESTALE</code></td>
    <td>表明一个过期的文件句柄引用。</td>
  </tr>
  <tr>
    <td><code>WSAEREMOTE</code></td>
    <td>表明项目是远程的。</td>
  </tr>
  <tr>
    <td><code>WSASYSNOTREADY</code></td>
    <td>表明网络子系统未就绪。</td>
  </tr>
  <tr>
    <td><code>WSAVERNOTSUPPORTED</code></td>
    <td>Indicates that the <code>winsock.dll</code> version is out of
    range.</td>
  </tr>
  <tr>
    <td><code>WSANOTINITIALISED</code></td>
    <td>表明 WSAStartup 尚未被成功执行。</td>
  </tr>
  <tr>
    <td><code>WSAEDISCON</code></td>
    <td>表明正在进行正常关机。</td>
  </tr>
  <tr>
    <td><code>WSAENOMORE</code></td>
    <td>表明没有更多结果。</td>
  </tr>
  <tr>
    <td><code>WSAECANCELLED</code></td>
    <td>表明操作已被取消。</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROCTABLE</code></td>
    <td>表明过程调用表是无效的。</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROVIDER</code></td>
    <td>表明无效的服务提供者。</td>
  </tr>
  <tr>
    <td><code>WSAEPROVIDERFAILEDINIT</code></td>
    <td>表明服务提供者初始化失败。</td>
  </tr>
  <tr>
    <td><code>WSASYSCALLFAILURE</code></td>
    <td>表明系统调用失败。</td>
  </tr>
  <tr>
    <td><code>WSASERVICE_NOT_FOUND</code></td>
    <td>表明无法找到服务。</td>
  </tr>
  <tr>
    <td><code>WSATYPE_NOT_FOUND</code></td>
    <td>表明类类型无法找到。</td>
  </tr>
  <tr>
    <td><code>WSA_E_NO_MORE</code></td>
    <td>表明没有更多结果。</td>
  </tr>
  <tr>
    <td><code>WSA_E_CANCELLED</code></td>
    <td>表明调用已被取消。</td>
  </tr>
  <tr>
    <td><code>WSAEREFUSED</code></td>
    <td>表明数据库查询被拒绝。</td>
  </tr>
</table>

### dlopen Constants

If available on the operating system, the following constants are exported in `os.constants.dlopen`. See dlopen(3) for detailed information.

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>RTLD_LAZY</code></td>
    <td>Perform lazy binding. Node.js sets this flag by default.</td>
  </tr>
  <tr>
    <td><code>RTLD_NOW</code></td>
    <td>Resolve all undefined symbols in the library before dlopen(3)
    returns.</td>
  </tr>
  <tr>
    <td><code>RTLD_GLOBAL</code></td>
    <td>Symbols defined by the library will be made available for symbol
    resolution of subsequently loaded libraries.</td>
  </tr>
  <tr>
    <td><code>RTLD_LOCAL</code></td>
    <td>The converse of <code>RTLD_GLOBAL</code>. This is the default behavior
    if neither flag is specified.</td>
  </tr>
  <tr>
    <td><code>RTLD_DEEPBIND</code></td>
    <td>Make a self-contained library use its own symbols in preference to
    symbols from previously loaded libraries.</td>
  </tr>
</table>

### Priority Constants<!-- YAML
added: v10.10.0
-->The following process scheduling constants are exported by `os.constants.priority`.

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>PRIORITY_LOW</code></td>
    <td>The lowest process scheduling priority. This corresponds to
    <code>IDLE_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>19</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_BELOW_NORMAL</code></td>
    <td>The process scheduling priority above <code>PRIORITY_LOW</code> and
    below <code>PRIORITY_NORMAL</code>. This corresponds to
    <code>BELOW_NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>10</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_NORMAL</code></td>
    <td>The default process scheduling priority. This corresponds to
    <code>NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>0</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_ABOVE_NORMAL</code></td>
    <td>The process scheduling priority above <code>PRIORITY_NORMAL</code> and
    below <code>PRIORITY_HIGH</code>. This corresponds to
    <code>ABOVE_NORMAL_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-7</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGH</code></td>
    <td>The process scheduling priority above <code>PRIORITY_ABOVE_NORMAL</code>
    and below <code>PRIORITY_HIGHEST</code>. This corresponds to
    <code>HIGH_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-14</code> on all other platforms.</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGHEST</code></td>
    <td>The highest process scheduling priority. This corresponds to
    <code>REALTIME_PRIORITY_CLASS</code> on Windows, and a nice value of
    <code>-20</code> on all other platforms.</td>
  </tr>
</table>

### libuv 常量

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>UV_UDP_REUSEADDR</code></td>
    <td></td>
  </tr>
</table>

