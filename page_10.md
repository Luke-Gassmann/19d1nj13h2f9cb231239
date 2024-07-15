https://www.ibm.com/docs/en/storage-fusion-software/2.8.x?topic=overview-verifying-image-signatures



Verifying image signatures
Digital signatures provide a way for consumers of content to ensure that what they
download is both authentic (it originated from the expected source) and has integrity (it is what we
expect it to be). All images for IBM Storage Fusion are
signed. This page describes how to verify the signatures on those images.
Before you begin
Your machine must have these command line tools installed (they can usually be installed on Linux
using the package manager):


GNU Privacy Guard v2


OpenSSL


skopeo


The IBM Storage Fusion public key must exist on the same
machine. Copy the following into a text editor, and save it in a file named
storage-fusion.pub.asc:
-----BEGIN PGP PUBLIC KEY BLOCK-----

mQINBGPOH0IBEADA253RAyBkEFFO7d9gfu+hdG58qQUe2H+4m5MuLc0zy/ulhkGg
YGBWFBCutkMp9F/jvtTrhf8r0oSlrIIzyJHFpM6qnlLftkbzQlpaj8yT+aPpNgVm
1xF5+hS32ouPXlUfaP3sX5CL0VZ44UhL0FBszfps7EPQU4C9fp6Rwstgejt+k5Xc
LIGiUIa+Kr3bmrBqN8nhsTE5csMlzS6tAIiG1R1I3qGRVcICpPh3lN7Mw2PYH8mB
kr0+a5pWQLJa/XSac9VHoDxoLCY8aPuxfLZUbTKEVkuGMXWvBHPVNYScydos5Jd9
Lzpc5uP6a8+7SBdMGZ5rupVkDKAZRTn+bxvI49D1yO0DBbXLaOMYevXUCIDeq3DI
X5BLNUZy8j6283IEReBTol8HnefpCT4mXQijFCIk595JiZwbcCY23XDdooXeTwk1
WZQI/TeQdV2q+gSS+tmdj3lD/iolXbNXneBK1G858sgct2hTIqZ/S2B3R94lDL2N
neV4IcsRy4r00bG2OdyLX/24yV857U427s1X56zc740pYgF/Uu61dauviXyaU2UD
C2KBy/YWmpWaMAeqNLRRYcHCUb9HZCfWchPlywXWIIggjL3D8vrPePWITpblC4wF
Tl6utwKHKM1CUqjn20j6q2Mh/7Z7g5XwaqmtoDm8cpx1bRY2ChHHxPXzbQARAQAB
tCpJQk0gU3BlY3RydW0gRnVzaW9uIEhDSSA8cHNpcnRAdXMuaWJtLmNvbT6JAjoE
EwEIACQFAmPOH0ICGw8FCwkIBwIGFQoJCAsCBBYCAwECHgEFCQPCZv8ACgkQHS4H
jVltgQNUmQ/+J9xUtUs1PwzAB/LpoqHGOmyZqz6EmQbaRiPzD4VSxcTYbpSKVb07
5H1sVR0QgDR9OUt5cbc4d9NBtFGiY8UeiCSL+MPjy5ksjFmbsxLRKEYZjB/qiOHv
c8viMH4y0boquomjeqGL1qajKyUvG1h99S5osGJVmPa2tmxMhTai57+aDX5SAKS4
RO1fd52K4nZw5+iqy95fXoEkPNwdw6Xm2fZ10F+kZ2dS8y+gu45hEaa/h+3P2myJ
37mp+336cfrqmqIv0pXD64et8zsQRNYqr2QEUSNsJ7ok4RkRqlpku5RYTV7T7TqH
g88rLAY1vxw4RzkQMve+t1IqgLANG9A+/fbQUQ/yshjCmvqmzB54VrOjOIwMWVtL
J+u1jbrdX1kFPogei6c0v3CBNe1khO6+1amBPTazKONbuMhBvaseX16x4Mk5r0FS
4FLNDEjktk4qUQAkEZk/Sugozp6oQpMYmKxPIt/7snLL9e6naF98TosKrpUCkme3
phbRIsML7Z7rUWg+jGS0Iz2L4FnVGrFs8iKsq23jvAf02nTKPtfgbozp6wMRC/KL
Wn3d9bGePGCMwPNwn3Auo8w/qMvHNAHykwTq1T1r/1vrmOnx+EEar2J2ZXqoA82P
4hcXWG4auoSA3y9tjAVLWChZdawFcMqcHZlHxER9/GOnY3hP+WSmv8o=
=YUDL
-----END PGP PUBLIC KEY BLOCK-----

You must have a list of images to verify. To get a list of container images
used, see the procedure in Installing IBM Storage Fusion from enterprise registry. 
In this procedure, the following example image is used:
icr.io/cpopen/isf-operator-catalog:2.8.0-linux.amd64. 

ProcedureRun the following command to delete all previous IBM Storage Fusion public keys:
 sudo gpg2 --delete-key "Fusion"To confirm the key deletion, enter 'Y'.
If you have previous IBM Storage Fusion public keys, repeat
this step until gpg2 reports: gpg: key "Fusion" not found: Not found
gpg: Fusion: delete key failed: Not found


Import the IBM Storage Fusion public key on the machine
that you prepared according to the Before you begin section:

sudo gpg2 --import storage-fusion.pub.asc
Note: This step must be done only once on each machine you use for signature verification.

Calculate the fingerprint: 
fingerprint=$(sudo gpg2 --fingerprint --with-colons "Fusion" | grep fpr | tr -d 'fpr:')
This command stores the key's fingerprint in an environment variable that is called
fingerprint, which is needed for the command to verify the signature. When you exit
your shell session, the variable gets deleted. The next time that you log in to your machine, you
can set it again by rerunning the command.

Create a directory for the image and use skopeo to pull it into local
storage: 
mkdir images
skopeo copy docker://icr.io/cpopen/isf-operator-catalog:2.7.1-linux.amd64 dir:./images
This command downloads the image as a set of files and places them in the images
directory (or another directory that you choose).Note: There is a manifest file that is named
images/manifest.json, and a signature file named
images/signature-1. You reference both these files in the next step (in the command
to verify the signature).

Log in to the icr.io entitlement registry to pull the image. Alternatively, you
can pass your credentials directly to skopeo with --src-creds
iamapikey:<YOUR ENTITLEMENT KEY>.

Verify the signature: 
sudo skopeo standalone-verify ./images/manifest.json icr.io/cpopen/isf-operator-catalog:2.8.0-linux.amd64 ${fingerprint} ./images/signature-1

Signature verified, digest sha256:0000000000000000000000000000000000000000000000000000000000000000






Parent topic: Product overview






