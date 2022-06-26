<h2> Express Cheatsheet</h2>
<table>
  <tr><th>express<th>application</tr>
  <tr>      
    <td valign="top"><pre>
var express = require('express')
express.json(opts) // middleware
express.raw(opts) // middleware
express.static(root, opts) // mideleware
express.text(opts) // middleware
express.urlencoded(opts) // mideleware
express.Router() -> Router</pre></td>
    <td valign="top"><pre>
var appp = require('express').express()
app.locals.title = 'My App
app.mountpath // '/my-path
app.on('mount', parent => {})
app.all(path, (req, res) => {})
app.delete(path, (req, res) => {})
app.get(path,  (req, res) => {})
app.post(path,  (req, res) => {})
app.put(path,  (req, res) => {})
app.listen(port, host, backlog, cb)
app.set('title', 'My Site')
app.get('title') // "My Site"
app.use(path, middleware)
app.use(middleware)
</pre></td>
  <tr>
  <tr><th>request<th>respnse</tr>
  <tr>      
    <td valign="top"><pre>
req.app.get('title') // "My Site"
req.baseUrl // /greet
req.body 
req.cookies.myCookie // 'value'
req.fresh // true
req.stale // true
req.hostname // example.com
req.subdomains // 'my' from 'my.domain.com'
req.method // GET
req.originalUrl // '/search?q=something'
req.params.id // '1'
req.protocol // 'http'
req.secure // true
req.signedCookies.user // 'tobi'

req.accepts(['html', 'json']) // "json"
req.accepts('image/png') // false
req.get('Content-Type') // "text/plain"
req.is('json') // 'json'
req.is('html') // false
req.param('name') // 'tobi'</pre>
    </td>
    <td valign="top"><pre>
res.app.get('title') // "My Site"
res.headersSent // false
res.locals.user = req.user

res.append('Set-Cookie', 'foo=bar;')f
res.attachment('path/to/logo.png')
res.cookie('name', 'tobi', opts)
res.clearCookie('name')
res.status(404).end()
res.format(object)
res.get('Content-Type') // 'text/plain'
res.status(500).json({ error: 'message' })
res.status(500).jsonp({ error: 'message' })
res.links(obj) // set Link header
res.location(path) // set Location header
res.redirect(301, 'http://example.com')
res.sendFile('index.html')
res.set('Content-Type', 'text/plain')</pre>
    </td>
  </tr>
  <tr><th>Router<th></tr>
  <tr>      
    <td valign="top"><pre>
router.all('/api/*', requireAuthentication)
router.delete(path, (req, res) => {})
router.get(path,  (req, res) => {})
router.post(path,  (req, res) => {})
router.put(path,  (req, res) => {})
router.route('/users/:user_id')
  .all(...).get(...).put(...).post(...)
router.use(middleware)
router.use('/bar', middleware)</pre>
    </td>
    <td valign="top"><pre></pre>
    </td>
  </tr>
</table>




  
