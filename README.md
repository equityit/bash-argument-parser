# BASH Argument Parser

Takes arguments passed in nearly any format to a bash script and allows easy access to them and their values

## Use

### Get An Arguments Value

```bash

	# -a "some text"
	if [ "$(argValue "a")" == 'some text' ]; then
		# Do something awesome
	fi
	
	# --debug 3
	DEBUG_LEVEL="$(argValue "debug")" # 3
	
	# -R 0
	[ "$(argValue "R")" == "0" ] && echo "Recursive depth 0"
	
	# -aXb 'cookie'
	BISCUIT="$(argValue "b")" # 'cookie'
	
```

### Check If An Argument Has Been Passed

There is a helper function named `argExists()` which takes the name of 
an argument as its only parameter and returns a boolean.

```bash
	
	# -v
	if argExists 'v'; then
    	echo "The -v argument has been passed"
    fi
    
    # -rMd
	argExists 'r' && echo "The -r argument was passed"
    
    # --long-argument-name
	if argExists 'long-argument-name'; then
    	# Do something awesome
    fi
    
    # -O 43
    argExists 'r' && echo "Found the -O argument"

```

Check for the `--test` flag

```bash

	if argExists 'test'; then
    	echo "The --test flag has been passed"
    fi
    
    # Or
    
    argExists 'test' && echo "Testing enabled"

```

## Supported Argument Formats

### Short Form

```bash
	-a
	-X
	-b somevalue
	-c 38
	-d "some value with spaces"
	-e "some value with
newlines"
```

### Long Form

```bash
	--debug
	--test mode0
	--test "all the code"
	--Case-Sensitive true
	--long-parameter
	--newline "
"
```

### Chained Short Form Arguments

```bash
	-aih	# Equivalent to -a -i -h
	-dav 4	# Equivalent to -d -a -v 4
```

## Argument Order

The order the arguments are passed on the command line makes a difference

### Examples

* Calling `my-script.sh -f first -f last` will cause `${args["f"]}` to have the value `last`
* Calling `my-script.sh -g 345 -g` will mean cause `${args["g"]}` to be blank

## Debug Mode

There is a debug mode that can be enabled by setting the `ARG_DEBUG` variable at the top of the script to `true`.
This will cause the script to dump out information about which flags it finds and of what kind etc