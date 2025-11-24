<link rel="stylesheet" href="assets/css/dark.css">

# Table of Contents

- [Procedural Models](#procedural-models)
  - [Functional Models](#functional-models)
  - [Behavioral Models](#behavioral-models)
  - [Process Statements](#process-statements)
    - [Initial Statements](#initial-statements)
    - [Always_comb](#always_comb)
    - [Always_latch](#always_latch)

## Combinational Logic Modeling

- There are 3 kinds modeling for combinational logic:
  - Structural (gate primitive intrinsics)
  - Dataflow (continuous assignments)
  - Behavioral (procedural blocks)

## Procedural Models

- Come in two flavors, functional or behavioral.
- execute sequentially like code.
- Describe synthesizeable functional blocks or testbenches
- Are described by process statements

### Functional Models

- As name implies, think functions.
- Run in 0 sim time and must have no timing specifications.
- Only kind of procedural models that are synthesizeable.

### Behavioral Models

- Allow for a sequence of scheduled (timing wise) actions
- Allow for timing specifications, ex:
  - #(time delay)
  - @(event control) such as a clock
  - wait(some time)

### Process Statements

- Always concurrent
- Typically used ones are:
  - `always_comb`, combinational logic
  - `always_ff`, edge triggered logic
  - `always_latch`, level sensitive. The only time you want a latch is when you
  are intentional describing one.
  - `initial`, executed first at sim time 0. Used to initialize default values
  - `final`, executed as the last block of the simulation

#### Initial Statements

- Run once and only once at sim start. At sim time 0.
- However there is a caveat, so called initial forever statements:

```systemVerilog
    initial
    begin
        vIf.clk = 1'b0;
        forever #20 vIf.clk = ~vIf.clk;
    end
```

These blocks are used for simulation constructs such as clocks

#### Always_comb

- All the variables used on the RHS are automatically part of the block's
sensitivity list. Just as if you have done an `always(*)`.
- Variables that are passed into functions that are called inside the block are
also part of the sensitivity list.
- Variables that are written to inside any process block cannot be written to by
another.
- `always_comb` blocks will always run at the start of a sim, sim time 0, after
initial processes.
- Cannot contain time control statements such as #(time delay),
@(event control), or wait statements

#### Always_latch

In the very rare instances you want a latch, use `always_latch`. It follows
similar sensitivity list rules as `always_comb`.
