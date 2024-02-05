Command Line Introduction: Excercises
======================================

## Excercise 1: Basic File Operations

<u>Tasks:</u>
1. Change to your home directory *(1 command)*
2. Create a file named ‘test.txt’ (and check if it is there) *(2 command)*
3. Create a directory named ‘tutorial’ *(1 command)*
4. Copy ‘test.txt’ into the directory ‘tutorial’ *(1 command)*
5. Delete ‘test.txt’ (in your home) *(1 command)*
6. Change to ‘tutorial’ and rename ‘test.txt’ to ‘file.txt’ and verify *(3 command)*
7. Remove the directory ‘tutorial’ and its contents *(3 command)*

<details><summary>Show solution</summary><pre><code>
cd
touch test.txt
ls -lrt
mkdir tutorial
cp test.txt tutorial/
rm test.txt
cd tutorial
mv test.txt file.txt
ls
rm file.txt
cd .. 
rmdir tutorial
</code></pre></details>

## Excercise 2: Links

<u>Tasks:</u>
1. change to /mnt/ *(1 command)*
2. Create a directory with the name “quality” and give it to the user ubuntu *(2 command)*
3. Go back to your home directory *(1 command)*
4. Create a soft link called ‘quality’ to /mnt/quality *(1 command)*

**Note:** this cannot be done using normal permission. use sudo for operating with root privileges

<details><summary>Show solution</summary><pre><code>
cd /mnt
sudo mkdir quality
sudo chown ubuntu:ubuntu quality
cd
ln -s /mnt/quality
</code></pre></details>
 
