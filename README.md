# nginx-config-tools

Tools for working with `nginx.conf`.

## Usage

```
usage:
    nginx-conf-flatten <mode> <source_file> <output_file|output_directory>
    
modes:
    
    flatten:
        flatten an nginx config file by inlining all includes recursively,
        save to <output_file>
        
    clean-directory:
        generate a cleaned nginx config directory, containing only the files
        that are included from the source file, or files included from those,
        and so on; output to <output_directory>
```

## FAQ

 - **why Bash? (Python|Ruby|Rust|OCaml|COBOL|FORTRAN) would have been so much (harder|better|faster|stronger)?**:  
   Mainly because of compatibility. I expect this tool to be useful in weird server/docker deployments where ability to install dependencies is limited. Bash is available by default in a lot of such environments.
 
