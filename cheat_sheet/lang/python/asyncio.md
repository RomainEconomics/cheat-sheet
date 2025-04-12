# Asyncio in Python

This:

```py
asyncio.run(f())
```

Roughly equivalent to:

```py
loop = asyncio.new_event_loop()
loop.create_task(f())
loop.run_until_complete()
```
