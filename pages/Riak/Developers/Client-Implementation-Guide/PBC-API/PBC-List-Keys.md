List all of the keys in a bucket. This is a streaming call, with multiple
response messages sent for each request.

## Request


```bash
message RpbListKeysReq {
    required bytes bucket = 1;
}
```


Optional Parameters

* **bucket** - bucket to get keys from

## Response


```bash
message RpbListKeysResp {
    repeated bytes keys = 1;
    optional bool done = 2;
}
```


Values

* **keys** - batch of keys in the bucket.
* **done** - set true on the last response packet

## Example

Request

```bash
Hex      00 00 00 0B 11 0A 08 6C 69 73 74 6B 65 79 73
Erlang <<0,0,0,11,17,10,8,108,105,115,116,107,101,121,115>>

RpbListKeysReq protoc decode:
bucket: "listkeys"

```


Response Pkt 1

```bash
Hex      00 00 00 04 12 0A 01 34
Erlang <<0,0,0,4,18,10,1,52>>

RpbListKeysResp protoc decode:
keys: "4"

```


Response Pkt 2

```bash
Hex      00 00 00 08 12 0A 02 31 30 0A 01 33
Erlang <<0,0,0,8,18,10,2,49,48,10,1,51>>

RpbListKeysResp protoc decode:
keys: "10"
keys: "3"
```


Response Pkt 3

```bash
Hex      00 00 00 03 12 10 01
Erlang <<0,0,0,3,18,16,1>>

RpbListKeysResp protoc decode:
done: true

```