# NEO Smart Contracts: Build & Test

This is a followup post to the hello world tutorial post, which will go over how to quickly build and test your smart contract code before importing.

If you haven’t already already gone though the hello world and the dev environment setup tutorials, I’d suggest you quickly run through those before continuing with this post.

Hello World Smart Contract Tutorial

Dev Environment Setup Tutorial

In the hello world tutorial we went over the steps on how to separately build and import a contract file. This exercise is useful for when you have your contract code built out to a reasonable level and would like to test it on your private net. However, there is a much quicker way to test your contract code without even importing it!

Within the neo-python cli there is a command build. We called it in the hello world tutorial in order to compile our py file into a avm file, with the following structure:
```
build path/to/file.py
```

The great news is that this build command also takes additional parameters, that combine a contract import and testinvoke.
```
build {path/to/file.py} test {input_types} {return_type} {needs_storage} {needs_dynamic_invoke} {test_param} ...
```

As you can see it looks very familiar to the contract import command, but also allows you to append all arguments to the end of the command to run your test. For example:
```
build smartContracts/helloWorld.py test "" 01 False False
```

Notice that the command references the .py file, and not the .avm file, when compared to contract import. This is because it will perform the compilation and test invocation of the new .avm in the same command.

Let’s take a look at a slightly more interesting contract for string concatenation.
```
from boa.code.builtins import concat
def Main(initialString, args):
    result = initialString
    for word in args:
        if result == None:
            result = word
        else:
            result = concat(result,' ')
            result = concat(result,word)
        print(result)
    return result
```

This contract take a two arguments, and initial string, and an Array. It iterates through every item in the array, and concatenates each value with the initial string. This then becomes the return value. In order to run this, we can use the following command:
```
build smartContracts/concat.py test 0710 07 False False sunshine ['hello','world','things','otherthings']
```

The input takes a two arguments, one of type String, represented by 07, the other of type Array, represented by 10, and the return type will be a String, represented by 07. For a full list of data type to byte mappings can be found in the official NEO documentation.

NEO Smart Contract: Parameter Types

Now that we know how to use the build command with test invoke, we can now quickly iterate on developing and testing new code without having to import the contract code at every step!
