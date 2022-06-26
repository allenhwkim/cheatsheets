
<h2> Mongodb Cheatsheet</h2>
<table>
  <tr><th>Connect MongoDB Shell<th>Helpers</tr>
  <tr>      
    <td valign="top"><pre>
mongo "mongodb://192.168.1.1:27017"
mongo mongodb+srv://cluster-name.abcde.mongodb.net/myDb</pre></td>
    <td valign="top"><pre>
show dbs
db
use <database_name>
show collections
load("myScript.js")
</pre></td>
  </tr>
  <tr><th>create/delete<th>read</tr>
  <tr>      
    <td valign="top"><pre>
db.coll.insertOne({name: "Max"})
db.coll.insert([{name: "Max"}, {name:"Alex"}])
db.coll.insert({date: ISODate()})</pre>
<pre>
db.coll.remove({name: "Max"})
db.coll.remove({name: "Max"}, {justOne: true})
db.coll.remove({})
db.coll.findOneAndDelete({"name": "Max"})</pre>
    </td>
    <td valign="top"><pre>
db.coll.find({name: /^Max$/i})
db.coll.find({tags: {$all: ["Realm", "Charts"]}})
db.coll.find({field: {$size: 2}})
db.coll.find({results: {
  $elemMatch: {product: "xyz", score: {$gte: 8}}
}})

// Projections
db.coll.find({"x": 1}, {"actors": 1})
db.coll.find({"x": 1}, {"actors": 1, "_id": 0}) 
db.coll.find({"x": 1}, {"actors": 0, "summary": 0})

// Sort, skip, limit
db.coll.find({})
  .sort({"year": 1, "rating": -1})
  .skip(10)
  .limit(3)

// Read Concern
db.coll.find()
  .readConcern("majority")</pre>
    </td>
  </tr>
  <tr><th colspan="2">update</tr>
  <tr>      
    <td valign="top" colspan="2"><pre>
db.coll.update({"_id": 1}, {"year": 2016}) // WARNING! Replaces the entire document
db.coll.update({"_id": 1}, {$set: {"year": 2016, name: "Max"}})
db.coll.update({"_id": 1}, {$unset: {"year": 1}})
db.coll.update({"_id": 1}, {$rename: {"year": "date"} })
db.coll.update({"_id": 1}, {$inc: {"year": 5}})
db.coll.update({"_id": 1}, {$mul: {price: NumberDecimal("1.25"), qty: 2}})
db.coll.update({"_id": 1}, {$min: {"imdb": 5}})
db.coll.update({"_id": 1}, {$max: {"imdb": 8}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})

// Array
db.coll.update({"_id": 1}, {$push :{"array": 1}})
db.coll.update({"_id": 1}, {$pull :{"array": 1}})
db.coll.update({"_id": 1}, {$addToSet :{"array": 2}})
db.coll.update({"_id": 1}, {$pop: {"array": 1}})  // last element
db.coll.update({"_id": 1}, {$pop: {"array": -1}}) // first element
db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}})
db.coll.update({}, {$set: {"grades.$[element]": 100}}, {multi: true, arrayFilters: [{"element": {$gte: 100}}]})

// Update many
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

// FindOneAndUpdate
db.coll.findOneAndUpdate({"name": "Max"}, {$inc: {"points": 5}}, {returnNewDocument: true})

// Upsert
db.coll.update({"_id": 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true})

// Replace
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

// Save
db.coll.save({"item": "book", "qty": 40})

// Write concern
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})</pre>
    </td>
  </tr>
  <tr><th>Create Collection<th>Drop/Rename/stats Collection</tr>
  <tr>      
    <td valign="top"><pre>
db.createCollection("contacts", {
   validator: {$jsonSchema: {
      bsonType: "object",
      required: ["phone"],
      properties: {
         phone: {
            bsonType: "string",
            description: "required"
         },
         email: {
            bsonType: "string",
            pattern: "@mongodb\.com$",
            description: "match pattern"
         },
         status: {
            enum: [ "Unknown", "Incomplete" ],
            description: "must be one of enum"
         }
      }
   }}
})</pre></td>
    <td valign="top">
<pre>
db.coll.drop()
db.dropDatabase()
</pre>
<pre>
db.coll.stats()
db.coll.storageSize()
db.coll.totalIndexSize()
db.coll.totalSize()
db.coll.validate({full: true})
db.coll.renameCollection("new_coll", true)
</pre>
  </td></tr>
  <tr><th>Create Index<th>List/Drop/Hide Index</tr>
  <tr>      
    <td valign="top"><pre>
// Index Types
db.coll.createIndex({"name": 1})
db.coll.createIndex({"name": 1, "date": 1})
db.coll.createIndex({foo: "text", bar: "text"})
db.coll.createIndex({"$**": "text"}) // wildcard
db.coll.createIndex({"userMetadata.$**": 1})
db.coll.createIndex({"loc": "2d"})   // 2d index
db.coll.createIndex({"loc": "2dsphere"})

// Index Options
db.coll.createIndex( // TTL index
  {"lastModifiedDate": 1}, 
  {expireAfterSeconds: 3600}
)
db.coll.createIndex({"name": 1}, {unique: true})
db.coll.createIndex({"name": 1}, { // partial
  partialFilterExpression: {age: {$gt: 18}}
}) // partial index
db.coll.createIndex({"name": 1}, {
  collation: {locale: 'en', strength: 1}
}) 
db.coll.createIndex({"name": 1 }, {
  sparse: true
})</pre></td>
    <td valign="top">
      <pre>
db.coll.getIndexes()
db.coll.getIndexKeys()</pre>
      <pre>
db.coll.dropIndex("name_1")</pre>
      <pre>
db.coll.hideIndex("name_1")
db.coll.unhideIndex("name_1")</pre>
    </td>
  </tr>  
  <tr><th>Handy commands<th>Change Streams
</tr>
  <tr>      
    <td valign="top"><pre>
use admin
db.createUser({
  "user": "root", 
  "pwd": passwordPrompt(), 
  "roles": ["root"]
})
db.dropUser("root")
db.auth( "user", passwordPrompt() )

use test
db.getSiblingDB("dbname")
db.currentOp()
db.killOp(123) // opid

db.fsyncLock()
db.fsyncUnlock()

db.getCollectionNames()
db.getCollectionInfos()
db.printCollectionStats()
db.stats()

db.getReplicationInfo()
db.printReplicationInfo()
db.isMaster()
db.hostInfo()
db.printShardingStatus()
db.shutdownServer()
db.serverStatus()

db.setSlaveOk()
db.getSlaveOk()

db.getProfilingLevel()
db.getProfilingStatus()
db.setProfilingLevel(1, 200)

db.enableFreeMonitoring()
db.disableFreeMonitoring()
db.getFreeMonitoringStatus()

db.createView("viewName", "sourceColl", [
  {$project:{department: 1}}
])</pre></td>
    <td valign="top"><pre>
watchCursor = db.coll.watch([
  {$match : {"operationType" : "insert" } }
])

while (!watchCursor.isExhausted()){
  if (watchCursor.hasNext()){
    print(tojson(watchCursor.next()));
  }
}</pre></td>
  </tr>
  <tr><th>Replica Set<th>Sharded Cluster
</tr>
  <tr>      
    <td valign="top"><pre>
rs.status()
rs.initiate({"_id": "replicaTest",
  members: [
    { _id: 0, host: "127.0.0.1:27017" },
    { _id: 1, host: "127.0.0.1:27018" },
    { _id: 2, host: "127.0.0.1:27019", arbiterOnly:true }]
})
rs.add("mongodbd1.example.net:27017")
rs.addArb("mongodbd2.example.net:27017")
rs.remove("mongodbd1.example.net:27017")
rs.conf()
rs.isMaster()
rs.printReplicationInfo()
rs.printSlaveReplicationInfo()
rs.reconfig(<valid_conf>)
rs.slaveOk()
rs.stepDown(20, 5)</pre></td>
    <td valign="top"><pre>
sh.status()
sh.addShard("rs1/mongodbd1.example.net:27017")
sh.shardCollection("mydb.coll", {zipcode: 1})

sh.moveChunk("mydb.coll", 
  { zipcode: "53187" }, "shard0019")
sh.splitAt("mydb.coll", {x: 70})
sh.splitFind("mydb.coll", {x: 70})
sh.disableAutoSplit()
sh.enableAutoSplit()

sh.startBalancer()
sh.stopBalancer()
sh.disableBalancing("mydb.coll")
sh.enableBalancing("mydb.coll")
sh.getBalancerState()
sh.setBalancerState(true/false)
sh.isBalancerRunning()

sh.addTagRange("mydb.coll", 
  {state: "NY", zip: MinKey }, 
  { state: "NY", zip: MaxKey }, 
  "NY")
sh.removeTagRange("mydb.coll", 
  {state: "NY", zip: MinKey }, 
  { state: "NY", zip: MaxKey }, 
  "NY")
sh.addShardTag("shard0000", "NYC")
sh.removeShardTag("shard0000", "NYC")

sh.addShardToZone("shard0000", "JFK")
sh.removeShardFromZone("shard0000", "NYC")
sh.removeRangeFromZone("mydb.coll", 
  {a: 1, b: 1}, 
  {a: 10, b: 10})</pre></td>
  </tr>
</table>
