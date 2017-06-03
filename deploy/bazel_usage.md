## Use Bazel

### Workspace, Package and Targets
#### WORKSPACE
- All Bazel builds take place in a workspace
- The location of workspace contains a file called *WORKSPACE* in the top-level directory
- *WORKSPACE* file can be used to reference external dependencies
- *new_* repository funtions


#### Package
- a directory contains related files and specification of dependencies among them
- a directory contains a file named BUILD


#### Target
- label:
- types:
    1. files
        1. source files
        1. generated files
    2. rules: specify relationship between a set of input and a set of output files
    3. package groups



### Source files

#### C++
1. header

2. cpp
    - when include header files: use relative path starting from a folder or file in the top-level directory


### BUILD

#### Path reference
1. Depend Path in BUILD file
    1. *:target_path*: dependency on a target in the same directory
    1. *//lib_path:target_path*: dependency on a target from a full path from root

1. Only direct dependencies need to be specified as dependencies

1. Every cpp file is one target, and the dependency also define the target name rather than the header file

1. Adding include paths, sometimes one do not want include from root directory
    - e.g. `[-Ifolder1/folder2]`

1. Including external libraries


#### Outputs
1. bazel-bin

1. bazel-out

1. bazel-{prj_name}

1. bazel-genfiles

1. baze-testlogs

