# Developer rules
- Avoid keep unfinished branches
- Early test with real data
- Automate repetitive tasks
- Persist intermediate data
- Group data in embedded sub-entities
- Use TODO and FIXME

## Common bugs
- Caching all values: Solved by using conditions about what values are valid to be cached
- Forget to configure timezone: Solved by explicitly configuring the timezone
- Avoid to validate in local because is complex: Solved by having a friendly local app config
- Mistake variables with similar names: Solved by reviewing code before commit and merge
- Not having automated CI tasks: Solved by defining CI jobs
