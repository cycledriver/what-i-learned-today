---
title: "The Walrus Strikes Again"
date: 2025-10-16
---

## Walrus in New Places

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
from unittest.mock import Mock()
import pytest
import foo.bar

def test_foo(monkepatch: pytest.MonkeyPatch) -> None:
    mock_thing = Mock()
    monkeypatch.setattr(foo.bar, "baz", mock_thing)
    run_something()
    assert mock_thing.called
```

The other day I thought to myself, maybe I can use the walrus here...

```python
from unittest.mock import Mock()
import pytest
import foo.bar

def test_foo(monkepatch: pytest.MonkeyPatch) -> None:
    monkeypatch.setattr(foo.bar, "baz", mock_thing := Mock())
    run_something()
    assert mock_thing.called
```

Voila!  It works...  So, I learned that you can use the walrus operator in all types of places I hadn't considered.  
I've been using it in `if` and `while` statements to initialize and check but not in other types of expressions.

That's what I learned today...

## Something else I learned...

In researching for this post, I also learned something new.

I've also use the `pytest-mock` plugin on many projects but forgot how it helps simplify monkeypatching:

```python
# uv add --group dev pytest-mock
import foo.bar

def test_foo(mocker) -> None:
    mocker.patch("foo.bar.baz")
    run_something()
    foo.bar.baz.assert_called
```
