
#Low-Level HTTP Workshop

Raw HTTP Request to `reddit.com`

```
GET / HTTP/1.1
Host: reddit.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.10; rv:29.0) Gecko/20100101 Firefox/29.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Cookie: reddit_first=%7B%22organic_pos%22%3A%201%2C%20%22firsttime%22%3A%20%22first%22%7D
Connection: keep-alive
```

Raw HTTP Request to `localhost:3000/dogs`

```
GET /dogs HTTP/1.1
Host: localhost:3000
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.10; rv:29.0) Gecko/20100101 Firefox/29.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
```


#Rack

One Step Above Raw HTTP, Rack and the env hash

```
class Hello
  def self.call(env)
    puts env
    [ 200,                              # 200 indicates success
      {"Content-Type" => "text/plain"}, # the hash of headers
      ["THIS IS THE RESPONSE BODY"]     # we wrap the body in an Array so
                                        # that it responds to `each`
    ]
  end
end

run Hello
```

Next Level Rack, using a Request Object:

```
request = Rack::Request.new(env)
```

Let's send some different types of requests!

```
curl "localhost:9292"
```

```
curl -d "param1=value1&param2=value2" "localhost:9292"
```



#Exercise Specs


```
require 'spec_helper'
require_relative "../lib/request"

RSpec.describe 'Parser' do

  it "parses the verb" do
    input = [
      "POST /widgets/1/edit?some-id=42&some-other-id=other HTTP/1.1",
      "Host: localhost:3000",
      "Cache-Control: no-cache",
      "Content-Type: application/x-www-form-urlencoded",
      "",
      "first_name=Alex&last_name=Andrews"
    ].join("\n")

    request = Request.new(input)
    request.parse

    # get the body
    expect(request.body).to eq("first_name=Alex&last_name=Andrews")

    # get things from the request line
    expect(request.verb).to eq("POST")
    expect(request.path).to eq("/widgets/1/edit")
    expect(request.query_string).to eq("some-id=42&some-other-id=other")

    # parse the headers
    expect(request.headers).to eq({
      "Host" => "localhost:3000",
      "Cache-Control" => "no-cache",
      "Content-Type" => "application/x-www-form-urlencoded",
    })

    # bring together all the params
    expect(request.params).to eq({
      "some-id" => "42",
      "some-other-id" => "other",
      "first_name" => "Alex",
      "last_name" => "Andrews",
    })

  end

end

```
