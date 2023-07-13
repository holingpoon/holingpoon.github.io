---
layout: post
title: AWS CLI madness, can't find all log groups edition
---

Expectation: Searching on AWS console should work the same way as querying on CLI right?

Reality: Just using search pattern [coder] (anything that contains the word 'coder' would only return 83 search results. On the console it says there are 222 matches. I.e.

```
aws logs describe-log-groups --profile profilename --log-group-name-pattern [coder]
```

Would only return 83 items.

Don't even get me started on how the name pattern does not understand [coder\-].
