# yubikey
# Fedora 33 and Centos 8 - Tested 20201203 RWT.
# 20201203 armonica17   Initial Revision

#*****************************************************************
#*  NOTE             NOTE           NOTE           NOTE          *
#*                                                               *
#*  The software and advice contained in this project could      *
#*  LOCK YOU OUT of the machine you run this on. This is not     *
#*  my fault. Backup your system first. Try this on a VM that    *
#*  you can restore. Know what you're doing.                     *
#*                                                               *
#*****************************************************************

Now with that out of the way:
This project is to help people implement yubikeys. What is a Yubikey? It's a physical usb key that allows you to use one time
passwords. Using this method not only will they need a key, they'll need a password. This will significantly increase the
security of the system. Having a password is useless. Please consult yubico's site on how to set up a yubikey.

This project does NOT use U2F. We want this to work remotely. I'll post a U2F method later. That's even more
secure as it will link up to the U2F on the yubikey. We want this to work remotely, so that won't work.

I know you want to get this to work *NOW*. Please read this stuff, it is short, to the point.

Files:
authorized_keys - populate this file with the keys you want root to have on the other machine. If you're not
                  using root for remote access (good for you), simply change it to the user you want to populate
                  these keys into.
yubikey_mappings - I pupulated this file with a couple of examples. WTH is it? Pop your yubikey into a usb
                   device. Now press the button. You'll see something like the example. You'll want the first
                   12 characters. That is your static part of your key. Every physical key is different.
                   If you don't set this up, I guarantee it won't work.
Files:
su, sudo, login, sshd - You must change the yubico line and enter in your ID and KEY. Easy to get from yubico.
                        You may see an = or other chars in the key. Don't worry, that's right. Beware if you
                        use a bash shell command to change KEY to the key it may fail. Be sure to verify
                        those files are right. Verify them again.
sshd-second_config - Fix the Match lines at the bottom to allow a network or just one host without
                     a yubikey. They will need a ssh key on they machine. What is this for?
                     It exists to allow ansible to continue to work. Just add an entry in your
                     ~/.ssh/config file to tell it to use port 2222. The idea is you can allow
                     connections ONLY from the ansible host. Of course if you're using a user
                     other than root, it'll break because it will also require the yubikey
                     to elevate privilege. IDK of a way to prevent that so far.

This ansible playbook will switch your normal ssh port of 22 such that it will require a yubikey and
a password. A second sshd server is started to allow ansible connections.

Now you should be ready. Please let me know if I omitted something or there is some constructive
criticism. None of the stuff I could find via google worked. I decided to put this github out to fix that.


