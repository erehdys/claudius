# Laws of C and C++

With CODE.md.

- **C++ is C with a few additions** (the user, 2026-10-23; the dialect of
Casey Muratori and Jonathan Blow). Plain structs of data and free
functions. A feature is used only when it is necessary and its C
equivalent is longer and no clearer:
  - USED: namespaces; references as pointers that cannot be null;
    `std::vector` as an array that knows its length; designated
    initializers; enums; function pointers; range-for; operator
    overloading for math types only (vector arithmetic).
  - NOT USED: lambdas and capture lists; writing templates;
    `std::function`; `auto` where the type is not visible; inheritance,
    virtual functions, classes that hide state behind methods;
    exceptions; RTTI; smart pointers; iostream. Other standard
    containers (`std::map`, `std::set`) only where an ordered lookup is
    the job. No macros.
  - INTEGERS: fixed widths (`int32_t`, `int64_t`, `uint8_t`) in every
    struct and column; a plain `int` only as the index of a short loop.
    Counts and indexes are signed: an unsigned subtraction below zero
    wraps round without a sound.
  - DIVISION: `/` and `%` cut toward zero, so -7 / 2 is -3. A value that
    can be negative is divided with a floor helper (in hvejs `fdiv` and
    `posmod`, `hex.cpp`); a raw `/` or `%` on such a value is a defect.
  - A function used in one file only is `static`; a constant is
    `constexpr`, never a `#define`.
  - ABSENT IS -1. Zero is a value: entity 0, row 0, spec 0 are real.
    Every struct member that can be absent has `= -1` in its
    declaration; raw zeroed memory is never read as a struct before its
    defaults are written.
