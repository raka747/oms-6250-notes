[link](http://frenetic-lang.org/publications/pyretic-login13.pdf)

# problem statement
- networks are hard to manage.  lots of low level config using vendor specific, low level apis

# solution
- use platform s/w to abstract out the difficult low level stuff
- write software logic in high level language

# understanding openflow
- interfaces switch hardware and user or middleware client
- define switch rules
    - header matching (for actions)
    - priority (against other rules)
    - action: flood, forward, drop, etc
    - etc etc

# pyretic basics
- define "policy" for packets via functional composition

The rest of the article goes into how policys can be defined using pyretic.
It's a semi-formal introduction to pyretic feature capabilities with justification of their practicality.
