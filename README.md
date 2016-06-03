# <strong>TagSee  - Making RFID Research Enjoyable!</strong>

## <strong>Version</strong>

<table>
    <tr>
	    <td><strong>Version</strong></td>
    	<td><strong>Description</strong></td>
        <td><strong>Released Time</strong></td>
        <td><strong>Download</strong></td>
    </tr>
    <tr>
	    <td>1.0</td>
    	<td>Manage physical reader and real-tiem view experimental results.</td>
        <td>2016/6/1</td>
        <td><a href="">TagSee-1.0.zip</a></td>
    </tr>
</table>


## <strong>Features</strong>

TagSee wraps the simple ImpinJ-extended APIs and offers a nice dashboard for quickly startup on collecting RFID readings. Basic useful feature list:

 * Manage your physical reader.
 * View experimental results in real-time.
 * Download experimental results.
 * Filter unexpected tags.

## <strong>Supported Platforms</strong>

* Windows/Mac/Linux
* ImpinJ R420 Reader

## <strong>Usage</strong>

1. Donwload tagsee-xxx.zip and extract it to local disk

2. Run the 'startup.sh' or 'startup.bat' in 'terminal' (Mac) or 'cmd' (Windows)

```bash
bash startup.sh
```

3. The system will automatically jump to dashboard page, or you can accesss the following address: <a href="http://localhost:9092">http://localhost:9092</a>

## <strong>Notice</strong>
Dashboard utilizes IndexDB, supported by browsers, to store the readings received from tagsee. The database size is limited over browsers. Please ensure you download the experimental results to your local disk in time.

## <strong>APIs</strong>

Besides controllable dashborad, TagSee also offers a set of wrapped APIs for upper applications.

### 1. Discover agents

```javascript

Path: /service/discover
Action: GET
Parameters: none
Returns:
	- errorCode: 0
	- agents[]: a list of agent stored in server.

```

### 2. Create agent
```javascript

Path: /service/agent/create
Action: POST
Paramters:
	- ip: reader ip, which should be
	- name: name of the reader.
	- remark: description of this reader.
Return:
	- errorCode: 0
```

### 3. Update agent
```javascript

Path: /service/agent/:ip/update
Action: POST
Parameters:
	- ip: reader ip.
	- name: the reader name.
	- remark: description of this reader.
Return:
	- errorCode: 0
```

### 4. Remove agent
```javascript

Path: /service/agent/:ip/remove 
Action: POST
Parameters:
	- ip: reader ip.
Return:
    - errorCode: 0
```

### 5. Start reading
```javascript

Path: /service/agent/:ip/start
Action: GET
Parameter: None
Return:
	- errorCode: 0
```

### 6. Stop reading
```javascript

Path: /service/agent/:ip/stop
Action: GET
Parameter: Nnone
Return:
	- errorCode: 0
```

### 7. Websocket messages

TagSee uses websocket to push heartbeat and readings.

```javascript

Message: Heartbeat
Structure:
	- errorCode: 0
	- type: heartbeat

Message: Readings
Structure:
	- errorCode: 0
	- type: reading
	- tags[{
		epc: tag epc,
        phase: pahse value,
        rssi: rss value,
        doppler: doppler value,
        channel: channel index,
        antenna: antenna idnex
        peekRssi: peek rssi (Impinj extened feild),
        firstSeenTime: the timestamp attached by the reader,
        lastSeenTime: the timestamp attached by the reader,
        timestap: the timestamp attached by the tagsee
    }]

```
