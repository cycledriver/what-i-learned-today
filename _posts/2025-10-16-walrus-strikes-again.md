---
title: "The Walrus Strikes Again"
date: 2025-10-16
---

I've been using the python walrus operator, `:=`, for some time now. It's a handy way to set and check at the same time:

```python
foo: dict[str, str] = {"a": 1}
if bar := foo.get("a"):
    print(f"a is {bar}"
```

This saves having to do this:
```python
foo: dict[str, str] = {"a": 1}
bar = foo.get("a")
if bar: 
    print(f"a is {bar}"
```

I've also been using pytest.monkeypatch with mocks for a long time and usually follow this pattern:

```python
def test_foo(monkepatch: pytest.MonkeyPatch) -> None:
    mock_thing = Mock()
    monkeypatch.setattr(foo.bar, "baz", mock_thing)
    run_something()
    assert mock_thing.called
```

The other day, I thought to myself, maybe I can use the walrus there...

def test_foo(monkepatch: pytest.MonkeyPatch) -> None:
    
    monkeypatch.setattr(foo.bar, "baz", mock_thing := Mock())
    run_something()
    assert mock_thing.called
```

Voila!  It works...

That's what I learned today...
