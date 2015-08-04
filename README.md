# rust-aws
AWS client libraries for Rust

## Current state

**Alpha**.  Rust code has been generated from JSON documentation of services from [botocore](https://github.com/boto/botocore).

## Installation / Setup
1. Install Rust 1.1.0 - http://www.rust-lang.org/
2. Check out code from github
3. Set up AWS credentials: environment variables (export AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY) or ~/.aws/credentials.
4. `cargo build`
5. `cargo run` - This will create real AWS resources and you may be charged.

#### Output from `cargo run` should resemble:

```
Existing queue: https://sqs.us-east-1.amazonaws.com/428250473290/test1
Existing queue: https://sqs.us-east-1.amazonaws.com/428250473290/test2
Created queue test_q_1436921723 with url https://sqs.us-east-1.amazonaws.com/428250473290/test_q_1436921723
Verified queue url https://sqs.us-east-1.amazonaws.com/428250473290/test_q_1436921723 for queue name test_q_1436921723
Send message with body 'lorem ipsum dolor sit amet' and created message_id 9315712d-3e6f-4264-95d4-426fe6a6f69f
Received message 'lorem ipsum dolor sit amet' with id 9315712d-3e6f-4264-95d4-426fe6a6f69f
Message deleted by request_id 2866edd9-d7ee-534b-9b43-a3c66653ef6e
Queue https://sqs.us-east-1.amazonaws.com/428250473290/test_q_1436921723 deleted by request_id b51e12e8-03dc-547c-aa7c-5cf7b261d6e1
Everything worked.
```

#### Example code in [src/bin/main.rs](src/bin/main.rs)

```rust
let sqs = SQSHelper::new(&creds, "us-east-1");

// list existing queues
let response = try!(sqs.list_queues());
for q in response.queue_urls {
  println!("Existing queue: {}", q);
}
```

#### Code generation

```bash
./botocore_parser path/to/some.json ClientClassName > some_module.rs
```