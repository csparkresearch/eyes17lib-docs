

## Set and Sense Logic Levels
Set/Sense logic levels on digital pins SQ1, SQ2, OD1, SEN*, IN2

### set_state : set a digital pin to HIGH (5V) /LOW (0V)

| parameter  | description                                 |
|------------|---------------------------------------------|
| \*\*kwargs |
|            | SQR1, SQR2, OD1 = False(LOW) or True( HIGH) |

!!! tip " Set SQ1 output to 5V, OD1 to 0V"
    ```python
    import eyes17.eyes
    p = eyes17.eyes.open()
    p.set_state(SQR1=True, OD1=False)
    ```


### get_states : get logic levels on digital input pins
`p.get_states()`

| Returns | description                                                        |
|---------|--------------------------------------------------------------------|
| dict    |
|         | {'IN2': T/F, 'SQR1': T/F, 'OD1': T/F, 'SEN': T/F, 'SQR1_OUT': T/F} |


!!! tip " Measure state of IN2"
    ```python
    import eyes17.eyes
    p = eyes17.eyes.open()
    states = p.get_states()
    print(f" IN2 is {'HIGH' if states['IN2'] else 'LOW'}")
    ```

??? info "Output for the above"
    <pre><font color="#008700">In [</font><font color="#33DA7A"><b>1</b></font><font color="#008700">]: </font><font color="#008700"><b>import</b></font> <font color="#0087D7"><b>eyes17.eyes</b></font>
    <font color="#008700">   ...: </font>p = eyes17.eyes.open()
    <font color="#008700">   ...: </font>states = p.get_states()
    <font color="#008700">   ...: print</font>(<font color="#AF5F00">f&quot; IN2 is </font><font color="#AF5F87"><b>{</b></font><font color="#AF5F00">&apos;HIGH&apos;</font><font color="#BCBCBC"> </font><font color="#008700"><b>if</b></font><font color="#BCBCBC"> </font>states[<font color="#AF5F00">&apos;IN2&apos;</font>]<font color="#BCBCBC"> </font><font color="#008700"><b>else</b></font><font color="#BCBCBC"> </font><font color="#AF5F00">&apos;LOW&apos;</font><font color="#AF5F87"><b>}</b></font><font color="#AF5F00">&quot;</font>)
     IN2 is HIGH
    
    <font color="#008700">In [</font><font color="#33DA7A"><b>2</b></font><font color="#008700">]: </font>states
    <font color="#870000">Out[</font><font color="#F66151"><b>2</b></font><font color="#870000">]: </font>
    {&apos;IN2&apos;: True,
     &apos;SQR1&apos;: False,
     &apos;OD1&apos;: False,
     &apos;SEN&apos;: True,
     &apos;SQR1_OUT&apos;: False,
     &apos;OD1_OUT&apos;: False,
     &apos;CCS&apos;: False}
    
    <font color="#008700">In [</font><font color="#33DA7A"><b>3</b></font><font color="#008700">]: </font>
    </pre>

### get_state : get logic level on any digital input pin
`p.get_state(channel)`

| Parameter | description             |
|-----------|-------------------------|
| channel   | 'IN2' , 'OD1', or 'SEN' |
| _Returns_ |
| bool      | True/False              |

??? "Example"
    <pre><font color="#008700">In [</font><font color="#33DA7A"><b>3</b></font><font color="#008700">]: </font>p.get_state(<font color="#AF5F00">&apos;SEN&apos;</font>)
    <font color="#870000">Out[</font><font color="#F66151"><b>3</b></font><font color="#870000">]: </font>True
    </pre>