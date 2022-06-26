Gobals: `__filename`, `__dirname`, `module`, `process`, `Buffer`.

Module:

      var module = require('./module.js')
      module.require('./my-module.js')
      module.id
      module.filename
      module.loaded
      module.parent
      module.children

<table>
  <tr>
    <td valign="top"><b>console</b></td>
    <td valign="top">
      console.log([data], [...])<br/>
      console.info([data], [...])<br/>
      console.error([data], [...])<br/>
      console.warn([data], [...])<br/>
      console.dir(obj)<br/>
      console.time(label)<br/>
      console.timeEnd(label)<br/>
      console.trace(label)<br/>
      console.assert(expression, [message])<br/>
    </td>
    <td valign="top"><b>timer</b></td>
    <td valign="top">
      setTimeout(callback, delay) <br/>
      clearTimeout(t)<br/>
      setInterval(callback, delay)<br/>
      clearInterval(t)<br/>
      setImmediate(callback)<br/>
      clearImmediate(obj)<br/>
      unref()<br/>
      ref()<br/>
    </td>
  </tr>
  <tr>
    <td valign="top"><b>process</b></td>
    <td valign="top"><pre>
process.on('exit', code=>{})
process.on('uncaughtException', err=>{})
process.stdout
process.stderr
process.stdin
process.argv
process.env
process.execPath
process.execArgv
process.arch
process.config
process.pid
process.platform
process.title
process.version
process.versions
process.abort()
process.chdir(dir)
process.cwd()
process.exit([code])
process.getgid()
process.setgid(id)
process.getuid()
process.setuid(id)
process.getgroups()
process.setgroups(grps)
process.initgroups(user, extra_grp)
process.kill(pid, [signal])
process.memoryUsage()
process.nextTick(callback)
process.maxTickDepth
process.umask([mask])
process.uptime()
process.hrtime()</pre>
    </td>
    <td valign="top"><b>child_process</b></td>
    <td valign="top" colspan="3"><pre>
const { spawn } = require('child_process');
const child = spawn('cmd.exe', ['/c', 'my.bat']);
child.stdin
child.stdout
child.stderr
child.pid
child.connected
child.kill([signal])
child.send(message, [sendHandle])
child.disconnect()
child_process.spawn(command, [args], [opts])
child_process.exec(command, [opts], cb)
child_process.execFile(file, [args], [opts], [cb])
child_process.fork(modulePath, [args], [opts]) 
    </td>
  </tr>
  <tr>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
  </tr>
  <tr>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
  </tr>
  <tr>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
  </tr>
  <tr>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
    <td valign="top"><b>title</b></td>
    <td valign="top">
      ...
    </td>
  </tr>
</table>




  
