#slide 
* Exactly same code locally as remote
* No networking bs
	* Bridge network, multiple levels of networking virtualization(win->wsl->docker)
* No OS virtualization 
	* No virtual filesystem, no virtual network stack, volume mounts, etc.
	* Just one binary per component
* Might be possible to make the repository dependencies self contained:
	* i.e. declarative local dev environment 
	* Reproducible local scripts/builds/tests 
	* POC: https://github.com/esoterra/wow/tree/main
	
``` sh
$ cd myREPO

# check tools needed in repo 
$ cat wow.kdl

registry "wow.wa.dev"

tool "cowsay" package="wow:cowsay"
tool "cat2" package="wow:kitty"

# pull tools into current shell
$ wow init

# use tools
$ cowsay hello
 _______
< HELLO >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
