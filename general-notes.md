# Mirror website with wget
wget -mkEpnp http://www.yoursite.org
# Curl - Test web connections from console and view returned results
curl -kis  http://xxx.xxx.xxx.xxx/etc/passwd
# Find Writable Directories (Good for uploading shells)
find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \;

find / -type d \( -perm -g+w -or -perm -o+w \) -exec ls -adl {} \; | grep www-data