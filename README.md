## INIFileParser for CMake



### Contents

- [What is this?](#what-is-this)



### What is this?

This is a CMake module that adds the function `parse_ini_file()` to your project. This function, when input the an INI-file

```ini
[system]
cores = 16
ram = 32

[other stuff]
number = 13, 33, 66
aString = I am a String!
```

will define the following variables in your scope

```
<PREFIX>_SECTIONS             = system;other_stuff

<PREFIX>_system_KEYS          = cores;ram
<PREFIX>_system_cores         = 16
<PREFIX>_system_ram           = 32

<PREFIX>_other_stuff_KEYS     = number;aString
<PREFIX>_other_stuff_number   = 13, 33, 66
<PREFIX>_other_stuff_aString  = I am a String!
```



