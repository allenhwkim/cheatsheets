Gobals: `__filename`, `__dirname`, `module`, `process`, `Buffer`.

<table>
  <tr><th>module<th>path</tr>
  <tr>      
    <td valign="top"><pre>
var module = require('./module.js')
module.require('./my-module.js')
module.id
module.filename
module.loaded
module.parent
module.children</pre></td>
    <td valign="top"><pre>
var path = require('path')
path.normalize(p)
path.join(...args)
path.resolve(...args, to)
path.relative(from, to)
path.dirname(p)
path.basename(p, [ext])
path.extname(p)
path.sep
path.delimiter</pre></td>
  <tr>
  <tr><th>console<th>timer</tr>
  <tr>      
    <td valign="top"><pre>
console.log([data], [...])
console.info([data], [...])
console.error([data], [...])
console.warn([data], [...])
console.dir(obj)
console.time(label)
console.timeEnd(label)
console.trace(label)
console.assert(expression, [message])</pre>
    </td>
    <td valign="top"><pre>
setTimeout(cb, delay)
clearTimeout(t)
setInterval(cb, delay)
clearInterval(t)
setImmediate(cb)
clearImmediate(obj)
unref()
ref()</pre>
    </td>
  </tr>
  <tr><th>process<th>fs</tr>
  <tr>
    <td valign="top"><pre>
process.on('exit', cb)
process.on('uncaughtException',cb)
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
    <td valign="top"><pre>

fs.rename(oldPath, newPath, cb)
fs.ftruncate(fd, len, cb)
fs.truncate(path, len, cb)
fs.chown(path, uid, gid, cb)
fs.fchown(fd, uid, gid, cb)
fs.lchown(path, uid, gid, cb)
fs.chmod(path, mode, cb)
fs.fchmod(fd, mode, cb)
fs.lchmod(path, mode, cb)
fs.stat(path, cb)
fs.lstat(path, cb)
fs.fstat(fd, cb)
fs.link(srcpath, dstpath, cb)
fs.symlink(srcpath, dstpath, [type], cb)
fs.readlink(path, cb)
fs.unlink(path, cb)
fs.realpath(path, [cache], cb)
fs.rmdir(path, cb)
fs.mkdir(path, [mode], cb)
fs.readdir(path, cb)
fs.close(fd, cb)
fs.open(path, flags, [mode], cb)
fs.utimes(path, atime, mtime, cb)
fs.futimes(fd, atime, mtime, cb)
fs.fsync(fd, cb)
fs.write(fd, buffer, offset, length, position, cb)
fs.read(fd, buffer, offset, length, position, cb)
fs.readFile(filename, [options], cb)
fs.writeFile(filename, data, [options], cb)
fs.appendFile(filename, data, [options], cb)
fs.watch(filename, [options], [listener])
fs.exists(path, cb)
fs.createReadStream(path, [options])
fs.createWriteStream(path, [options])</pre>
    </td>
  </tr>
  <tr><th>EventEmitter<th>child_process</tr>
  <tr>
    <td valign="top"><pre>
var EventEmitter = require('events')
var emitter = new MyEmitter()

emitter.addListener(e, cb)
emitter.on(e, cb)
emitter.once(e, cb)
emitter.removeListener(e, cb)
emitter.removeAllListeners([e])
emitter.setMaxListeners(n)
emitter.listeners(e);
emitter.emit(event, ...args)</pre>
    </td>
    <td valign="top"><pre>
const { spawn } = require('child_process');
const child = spawn('ls', ['-al']);
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
child_process.execFile(file, [args], [opts])
child_process.fork(modulePath, [args], [opts])</pre>
    </td>
  </tr>
  <tr><th>Readable Stream<th>Writable Stream</tr>
  <tr>
    <td valign="top"><pre>
const { Readable } = require('stream')
const readable = new Readable()
readable.on('readable', cb)
readable.on('data', cb)
readable.on('end', cb)
readable.on('close', cb)
readable.on('error', cb)
readable.read([size]);
readable.setEncoding(encoding)
readable.resume()
readable.pause()
readable.pipe(dest, [opts])
readable.unpipe([dest])
readable.unshift(chunk)</pre>
    </td>
    <td valign="top"><pre>
const { Writable } = require('stream')
const writable = new Writable()

writable.write(chunk, [enc], [cb])
writer.once('drain', db)
writable.end([chunk], [enc], [cb])
writer.on('finish', cb)
writer.on('pipe', cb})
writer.on('unpipe', cb)
writer.on('error', cb)</pre>
    </td>
  </tr>

  <tr><th>fs.Stats<th>http</tr>
  <tr>
    <td valign="top"><pre>
stats.isFile();
stats.isDirectory()
stats.isBlockDevice()
stats.isCharacterDevice()
stats.isSymbolicLink()
stats.isFIFO()
stats.isSocket()</pre>
    </td>
    <td valign="top"><pre>
http.STATUS_CODES
http.request(opts, [callback])
http.get(opts, [callback])
server = http.createServer([requestListener])
server.listen(port, [hostname], [backlog], [cb])
server.listen(path, [callback])
server.listen(handle, [callback])
server.close([callback]) 
server.setTimeout(msecs, callback)
server.maxHeadersCount
server.timeout
server.on('request', (req,res)=>{})
server.on('connection', (socket)=>{})
server.on('close', cb)
server.on('checkContinue', (req,res)=>{})
server.on('connect', (req,socket,head)=>{})
server.on('upgrade',  (req,socket,head)=>{})
server.on('clientError', (req,socket)=>{})</pre>
    </td>
  </tr>
  <tr><th>request<th>response</tr>
  <tr>
    <td valign="top"><pre>
request.write(chunk, [enc])
request.end([data], [enc])
request.abort()
request.setTimeout(timeout, [cb])
request.setNoDelay([noDelay])
request.setSocketKeepAlive([enable], [delay])

request.on('response', resp => {})
request.on('socket', socket => {})
request.on('connect', (resp, socket, head) => {})
request.on('upgrade', (resp, socket, head) => {})
request.on('continue', cb)</pre> 
    </td>
    <td valign="top"><pre>
response.write(chunk, [enc])
response.writeContinue()
response.writeHead(status, [reason], [headers])
response.setTimeout(msecs, cb)
response.setHeader(name, value)
response.getHeader(name)
response.removeHeader(name)
response.addTrailers(headers)
response.end([data], [encoding])
response.statusCode
response.headersSent
response.sendDate

response.on('close', cb)
response.on('finish', cb)</pre>
    </td>
  </tr>
  <tr><th>url<th>querystring</tr>
  <tr>
    <td valign="top"><pre>
var url = require('url')
url.parse(url, [qs])
url.format(urlObj)
url.resolve(from, to);</pre> 
    </td>
    <td valign="top"><pre>
var querystring = require('querystring')
querystring.stringify(obj, [sep], [eq])
querystring.parse(str, [sep], [eq])</pre>
    </td>
  </tr>
  <tr><th>os<th>Buffer</tr>
  <tr>
    <td valign="top"><pre>
os.tmpdir()
os.endianness()
os.hostname()
os.type()
os.platform()
os.arch()
os.release()
os.uptime()
os.loadavg()
os.totalmem()
os.freemem()
os.cpus()
os.networkInterfaces()
os.EOL</pre> 
    </td>
    <td valign="top"><pre>
new Buffer(size)
new Buffer(array)
new Buffer(str, [enc])

Buffer.isEncoding(enc)
Buffer.isBuffer(obj)
Buffer.concat(list, [len])
Buffer.byteLength(string, [enc])

buf.write(str, [offset], [len], [enc])
buf.toString([enc], [start], [end])
buf.toJSON()
buf.copy(target, [sta], [srcSta], [srcEnd])
buf.slice([sta], [end])   
buf.fill(value, [offset], [end])
buf[index]
buf.length
buffer.INSPECT_MAX_BYTES</pre>
    </td>
  </tr>
</table>




  
