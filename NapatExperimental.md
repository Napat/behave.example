
**Reference**
- https://jenisys.github.io/behave.example/tutorials/


=============================

### Standard package and Built-in Functions

assert [condition]
"""
Raised error if condition return false: 

### Error if non-equivalent of value01 and value02 by using assert

assert [value01] is not [value02]
- Raised error if [value01] != [value02]
""" 

- getattr(object, name[, default])
getattr(x, 'foobar') is equivalent to x.foobar. If the named attribute does not exist, default is returned if provided, otherwise AttributeError is raised.

- If expected_object is not a class instance or an object of the given type then return False to assert error
assert isinstance(expected, int)

=============================
### Using pyhamcrest package

```
from hamcrest import assert_that, equal_to, is_not, greater_than
from hamcrest.library.collection.issequencegreater_than_containinginanyorder import contains_inanyorder
```

### Error if non-equivalent of value01 and value02 by using assert_that
`assert_that(theBiscuit, equal_to(myBiscuit))`

### Error if equivalent of value01 and value02 by using assert_that
`assert_that(context.ninja_fight, is_not(equal_to(None)))`

### UNORDERED TABLE-COMPARISON
`assert_that(contains_inanyorder(*expected_persons), actual_persons)`

### TABLE-SUBSET-COMPARISON 
`assert_that(has_items(*expected_persons), actual_persons)`

### using greater_than
`assert_that(context.duck_count, greater_than(0))`

=============================
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
### Using .... package
`from testutil import NamedNumber`

=============================
# [tutorial03]
### Both of feature file and python stepfile, step parameters should between double quotes


=============================
# [tutorial04]
## Outline parameter using `<>`

=============================
# [tutorial05: Passing Step data]

## Passing STEP-DATA to `context.text` of step argument.

```
**Causion**
STEP-DATA sis step scope, that's means we cannot use
context.text in other step (unlike user manual defined attributes). 
```
 
## Passing data between step using `context` attributes
```
**Note**
`context` attributes is scenario scope.
We cannot passing data to another scenarios using context attribute.
```

## `getattr()` is built-in Function that can throw error.

=============================
# [tutorial06: Passing Setup Table]

## Passing table to `context.table` of step argument.

```
**Note**
`context.table` is step scope, cannot use in other step. 
```

# Initial data pattern in senario level using `context` and `getattr()` 

```
reuse_var = getattr(context, "reuse_var", None)
    if not reuse_var:
        context.reuse_var = NewVarObj()
```

=============================
# [tutorial07: Setup Table]

### TABLE-SUBSET-COMPARISON (using: pyhamcrest)
```
expected_persons = [ row["name"]    for row in context.table ]
actual_persons   = department_.members
assert_that(has_items(*expected_persons), actual_persons)
```

=============================

# [tutorial08: Step executes other Steps]

```
#Syntax
context.execute_steps(u"""
        when I press the big {button_color} button
         and I duck
    """.format(button_color="red"))
```

```
from hamcrest import greater_than
assert_that(context.duck_count, greater_than(0))
```

=============================

# [tutorial09:  Using Background]

**BACKGROUND steps** are automatic called at begin of each scenario before other steps.

=============================

# [tutorial10: User-defined parameter type]

### User-defined parameter type
```
@when('I add "{x:Number}" and "{y:Number}"')
def step_impl(context, x, y):
    assert isinstance(x, int)
    ...
```

=============================

# [tutorial11: Using tags]

สามารถติด tags ให้กับ feature หรือ senario เพื่การใช้งานที่หลากหลายได้

### Example tags naming 
@wip    “Work in Process” (under development).
@skip   Skip/disable a feature, scenario, ...
@slow   Mark slow, long-running tests.

**Logic command options** 
select/enable       --tags=@one             Only items with this tag.
not (tilde/minus)   --tags=~@one            Only items without this tag.
logical-or          --tags=@one,@two        If @one or @two is present.
logical-and         --tags=@one --tags=@two If both @one and @two are present.

### Using select/enable tag: Execute only tag name `ninja.chuck`
```
$ behave --tags=ninja.chuck tutorial11_tags.feature
```

### Using not tag: Skip executing tag name `wip`
```
behave --tags=-wip tutorial11_tags.feature
```

### Using logical-or tag: Execute multiple tags `ninja.any` or `ninja.chuck`
```
$ behave --tags=@ninja.any,@ninja.chuck tutorial11_tags.feature
```

### Using logical-and tag: Execute anything that have both of `ninja.any` and `ninja.chuck` tags
```
behave --tags=@ninja.any --tags=@ninja.chuck tutorial11_tags.feature
```

=============================

# [tutorial12: Language]

สามารถเช็คภาษาอื่นๆที่ไม่ใช่ภาษาอังกฤษที่ behave framework ซัพพอตได้ด้วยคำสั่ง
`$ behave --lang-list`

หรือสามารถเข้าไปดูได้ที่ `<venv>\Lib\site-packages\behave\i18n.py`

ปัจจุบันไม่ support ภาษาไทย :p

=============================

