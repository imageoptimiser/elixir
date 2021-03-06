* enhancements
  * [Binary] Support `<< "string" :: utf8 >>` as in Erlang
  * [CLI] Support `--app` option to start an application and its dependencies
  * [ExUnit] ExUnit now supports multiple runs in the same process
  * [ExUnit] Failures in ExUnit now show a tailored stacktrace
  * [Kernel] Introduce `Application.Behaviour` to define application module callbacks
  * [Kernel] Introduce `Supervisor.Behaviour` to define supervisors callbacks
  * [Kernel] More optimisations were added to Record handling
  * [Mix] Mix now starts the current application before run, iex, test and friends

* bug fix
  * [String] `String.first` and `String.last` return nil for empty binaries
  * [String] `String.rstrip` and `String.lstrip` now verify if argument is a binary
  * [Typespec] Support ... inside typespec's lists

* deprecations
  * [OptionParser] `:flags` option was deprecated in favor of `:switches` to support many types

# v0.7.2 (2012-12-04)

* enhancements
  * [CLI] `--debug-info` is now true by default
  * [ExUnit] Make ExUnit exit happen in two steps allowing developers to add custom `at_exit` hooks
  * [IEx] Many improvements to helpers functions `h/1`, `s/1` and others
  * [Kernel] Functions defined with `fn` can now handle many clauses
  * [Kernel] Raise an error if clauses with different arities are defined in the same function
  * [Kernel] `function` macro now accepts arguments in `M.f/a` and `f/a` formats
  * [Macro] Improvements to `Macro.to_binary`
  * [Mix] Mix now echoes the output as it comes when executing external commands such as git or rebar
  * [Mix] Mix now validates `application` callback's values
  * [Record] Record accessors are now optimized and can be up to 6x faster in some cases
  * [String] Support `\xXX` and `\x{HEX}` escape sequences in strings, char lists and regexes

* bug fix
  * [Bootstrap] Compiling Elixir source no longer fails if environment variables contain utf-8 entries
  * [IEx] IEx will now wait for all command line options to be processed before starting
  * [Kernel] Ensure proper stacktraces when showing deprecations

* deprecations
  * [Enum] `Enum.qsort` is deprecated in favor of `Enum.sort`
  * [ExUnit] `assert left in right` is deprecated in favor of `assert left inlist right`
  * [List] `List.sort` and `List.uniq` have been deprecated in favor of their `Enum` counterparts
  * [Record] Default-based generated functions are deprecated
  * [Typespec] Enhancements and deprecations to the `@spec/@callback` and the fun type syntax

# v0.7.1 (2012-11-18)

* enhancements
  * [IEx] Only show documented functions and also show docs for default generated functions
  * [IO] Add `IO.binread`, `IO.binwrite` and `IO.binreadline` to handle raw binary file operations
  * [ExUnit] Add support for user configuration at `HOME/.ex_unit.exs`
  * [ExUnit] Add support for custom formatters via a well-defined behaviour
  * [Kernel] Add support for `defrecordp`
  * [Kernel] Improved dialyzer support
  * [Kernel] Improved error messages when creating functions with aliases names
  * [Mix] Improve SCM behaviour to allow more robust integration
  * [Mix] Changing deps information on `mix.exs` forces users to fetch new dependencies
  * [Mix] Support (parallel) requires on mix run
  * [Mix] Support `-q` when running tests to compile only changed files
  * [String] Support `String.downcase` and `String.upcase` according to Unicode 6.2.0
  * [String] Add support for graphemes in `String.length`, `String.at` and others
  * [Typespec] Support `@opaque` as attribute
  * [Typespec] Define a default type `t` for protocols and records
  * [Typespec] Add support for the access protocol in typespecs

* bug fix
  * [Kernel] Fix an issue where variables inside clauses remained unassigned
  * [Kernel] Ensure `defoverridable` functions can be referred in many clauses
  * [Kernel] Allow keywords as function names when following a dot (useful when integrating with erlang libraries)
  * [File] File is opened by default on binary mode instead of utf-8

* deprecations
  * [Behaviour] `defcallback/1` is deprecated in favor of `defcallback/2` which matches erlang `@callbacks`
  * [Enum] `Enum.times` is deprecated in favor of using ranges
  * [System] `halt` moved to `System` module

# v0.7.0 (2012-10-20)

* enhancements
  * [Behaviour] Add Behaviour with a simple callback DSL to define callbacks
  * [Binary] Add a Dict binary that converts its keys to binaries on insertion
  * [Binary] Optimize `Binary.Inspect` and improve inspect for floats
  * [CLI] Support `--detached` option
  * [Code] `Code.string_to_ast` supports `:existing_atoms_only` as an option in order to guarantee no new atoms is generated when parsing the code
  * [EEx] Support `<%%` and `<%#` tags
  * [ExUnit] Support `after_spawn` callbacks which are invoked after each process is spawned
  * [ExUnit] Support context data in `setup_all`, `setup`, `teardown` and `teardown_all` callbacks
  * [IEx] Support `after_spawn` callbacks which are invoked after each process is spawned
  * [Kernel] Better error messages when invalid options are given to `import`, `alias` or `require`
  * [Kernel] Allow partial application on literals, for example: `{ &1, &2 }` to build tuples or `[&1|&2]` to build cons cells
  * [Kernel] Added `integer_to_binary` and `binary_to_integer`
  * [Kernel] Added `float_to_binary` and `binary_to_float`
  * [Kernel] Many improvements to `unquote` and `unquote_splicing`. For example, `unquote(foo).unquote(bar)(args)` is supported and no longer need to be written via `apply`
  * [Keyword] Keyword list is no longer ordered according to Erlang terms but the order in which they are specified
  * [List] Add `List.keyreplace` and `List.keystore`
  * [Macro]  Support `Macro.safe_term` which returns `:ok` if an expression does not execute code and is made only of raw data types
  * [Mix] Add support for environments - the current environment can be set via `MIX_ENV`
  * [Mix] Add support for handling and fetching dependencies' dependencies
  * [Module] Support module creation via `Module.create`
  * [Range] Support decreasing ranges
  * [Record] Improvements to the Record API, added `Record.defmacros`
  * [Regex] Add `:return` option to `Regex.run` and `Regex.scan`
  * [String] Add a String module responsible for handling UTf-8 binaries

* bug fix
  * [File] `File.cp` and `File.cp_r` now preserves the file's mode
  * [IEx] Fix a bug where printing to `:stdio` on `IEx` was causing it to hang
  * [Macro] Fix a bug where quoted expressions were not behaving the same as their non-quoted counterparts
  * [Mix] `mix deps.get [DEPS]` now only gets the specified dependencies
  * [Mix] Mix now exits with status 1 in case of failures
  * [Protocol] Avoid false positives on protocol dispatch (a bug caused the dispatch to be triggered to an invalid protocol)

* backwards incompatible changes
  * [ExUnit] `setup` and `teardown` callbacks now receives the test name as second argument
  * [Kernel] Raw function definition with `def/4`, `defp/4`, `defmacro/4`, `defmacrop/4` now evaluates all arguments. The previous behaviour was accidental and did not properly evaluate all arguments
  * [Kernel] Change tuple-related (`elem` and `setelem`), Enum functions (`find_index`, `nth!` and `times`) and List functions (List.key*) to zero-index

* deprecations
  * [Code] `Code.require_file` and `Code.load_file` now expect the full name as argument
  * [Enum] `List.reverse/1` and `List.zip/2` were moved to `Enum`
  * [GenServer] Rename `GenServer.Behavior` to `GenServer.Behaviour`
  * [Kernel] Bitstring syntax now uses `::` instead of `|`
  * [Kernel] `Erlang.` syntax is deprecated in favor of simply using atoms
  * [Module] `Module.read_attribute` and `Module.add_attribute` deprecated in favor of `Module.get_attribute` and `Module.put_attribute` which mimics Dict API

# v0.6.0 (2012-08-01)

* incompatible changes
  * [Kernel] Compile files now follow `Elixir-ModuleName` convention to solve issues with Erlang embedded mode. This removes the `__MAIN__` pseudo-variable as modules are now located inside `Elixir` namespace
  * [Kernel] `__using__` callback triggered by `use` now receives just one argument. Caller information can be accessed via macros using `__CALLER__`
  * [Kernel] Comprehensions syntax changed to be more compatible with Erlang behavior
  * [Kernel] loop and recur are removed in favor of recursion with named functions
  * [Module] Removed data functions in favor of unifying the attributes API

* deprecations
  * [Access] The semantics of the access protocol were reduced from a broad query API to simple data structure key-based access
  * [ExUnit] Some assertions are deprecated in favor of simply using `assert()`
  * [File] `File.read_info` is deprecated in favor of `File.stat`
  * [IO] `IO.print` is deprecated in favor of `IO.write`
  * [Kernel] Deprecate `__LINE__` and `__FUNCTION__` in favor of `__ENV__.line` and `__ENV__.function`
  * [Kernel] Deprecate `in_guard` in favor of `__CALLER__.in_guard?`
  * [Kernel] `refer` is deprecated in favor of `alias`
  * [Module] `Module.add_compile_callback(module, target, callback)` is deprecated in favor of `Module.put_attribute(module, :before_compile, { target, callback })`
  * [Module] `Module.function_defined?` is deprecated in favor of `Module.defines?`
  * [Module] `Module.defined_functions` is deprecated in favor of `Module.definitions_in`

* enhancements
  * [Enum] Enhance Enum protocol to support `Enum.count`
  * [Enum] Optimize functions when a list is given as collection
  * [Enum] Add `find_index`, `nth!` and others
  * [ExUnit] Support setup and teardown callbacks
  * [IEx] IEx now provides autocomplete if the OS supports tty
  * [IEx] IEx now supports remsh
  * [IEx] Elixir now defaults to compile with documentation and `d` can be used in IEx to print modules and functions documentation
  * [IEx] Functions `c` and `m` are available in IEx to compile and print available module information. Functions `h` and `v` are available to show history and print previous commands values
  * [IO/File] Many improvements to `File` and `IO` modules
  * [Kernel] Operator `!` is now allowed in guard clauses
  * [Kernel] Introduce operator `=~` for regular expression matches
  * [Kernel] Compiled docs now include the function signature
  * [Kernel] `defmodule` do not start a new variable scope, this improves meta-programming capabilities
  * [Kernel] quote special form now supports line and unquote as options
  * [Kernel] Document the macro `@` and allow attributes to be read inside functions
  * [Kernel] Add support to the `%R` sigil. The same as `%r`, but without interpolation or escaping. Both implementations were also optimized to generate the regex at compilation time
  * [Kernel] Add `__ENV__` which returns a `Macro.Env` record with information about the compilation environment
  * [Kernel] Add `__CALLER__` inside macros which returns a `Macro.Env` record with information about the calling site
  * [Macro] Add `Macro.expand`, useful for debugging what a macro expands to
  * [Mix] First Mix public release
  * [Module] Add support to `@before_compile` and `@after_compile` callbacks. The first receives the module name while the latter receives the module name and its object code
  * [OptionParser] Make OptionParser public, add support to flags and improved switch parsing
  * [Range] Add a Range module with support to `in` operator (`x in 1..3`) and iterators
  * [Record] Allow `Record[_: value]` to set a default value to all records fields, as in Erlang
  * [Record] Records now provide a `to_keywords` function
  * [Regex] Back references are now properly supported
  * [System] Add `System.find_executable`

# v0.5.0 (2012-05-24)

* First official release