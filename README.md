# nginx-config-tools

Tools for working with `nginx.conf`.

## Usage

```
nginx-conf-flatten <mode> <input_file> <output_file|output_directory>
```

Modes are:
    
    `flatten`:
        flatten an nginx config file by inlining all includes recursively,
        save to <output_file>
        
    `clean-directory`:
        generate a cleaned nginx config directory, containing only the files
        that are included from the input file, or files included from those,
        and so on; output to <output_directory>

Imporant caveats:

 - `input_file` *must* exist (if it doesn't the script will exit with an error)
 - `output_file`/`output_directory` *must not* exist (if it does, the script will exit with an error)


## Operation

The script creates a temporary directory (`/tmp/nginx-conf-flatten.????`) and works in there.

Once output is ready (either in the form of a single flattened `nginx` config file if mode was `flatten`, or a directory structure if it was `clean-directory`), it is moved to the correct location and the temporary directory is removed.

The `flatten` mode makes an honest attempt at keeping indentation sane. This means looking at an `include` line, and indenting the text included from the relevant files by whatever indent was there in the `include` line. This seems to work reasonably well, but if you want the config to be linted and nicely formatted, use a linter and a formatter.

## FAQ

 - **Why Bash? (Python|Ruby|Rust|OCaml|COBOL|FORTRAN) would have been so much (harder|better|faster|stronger)?**  
   Mainly because of compatibility. I expect this tool to be useful in weird server/docker deployments where ability to install dependencies is limited. Bash is available by default in a lot of such environments.
 
 - **This is slow!**  
   And this is not a question!  
   Seriously though, yes, for large `nginx` configs with deeply nested includes it will take several seconds for the script to finish. There are surely ways to optimize this, and yes, if it was written in C it would be faster.
