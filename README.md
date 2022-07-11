# Unpacking UPX Packed Malware
Hash: fd6c69c345f1e32924f0a5bb7393e191b393a78d58e2c6413b03ced7482f2320
<img width="752" alt="Picture1" src="https://user-images.githubusercontent.com/107531426/178287960-38300fcd-99bf-4cfc-9c2e-47789893308a.png">
# Unpacking this with CMD
Use command “upx -d YourFileName” to unpack. 
And similarly if you want to Pack (Compress) any unpack file with UPX, use command just “upx YourFileName” to pack.

<img width="452" alt="Picture2" src="https://user-images.githubusercontent.com/107531426/178288948-a79b307a-7447-4c31-8f07-96e6adcafb47.png">
You will notice in the folder your Packed file is now replaced with unpacked file and if you compare this with previous one, the size, entrypoint, entropy, section all is changed. 
<img width="489" alt="pic4" src="https://user-images.githubusercontent.com/107531426/178289972-0555853f-824e-4f7c-99b3-832a6b36e8c9.PNG">
So Entrypoint and First Bytes of our Unpacked file is 

Entrypoint: 1CFE

First Bytes: 52,6A,36,68

# Checking this manually with x32dbg

# 1. Push Pop Method
Load sample in x32dbg and Run the Malware (F9). You’ll be at Entrypoint of your Binary (60 pushad)
<img width="752" alt="Picture6" src="https://user-images.githubusercontent.com/107531426/178291384-38ce7e5b-a3ce-4eed-98d1-218418508f6b.png">
<img width="752" alt="Picture7" src="https://user-images.githubusercontent.com/107531426/178291942-b602f67a-82d3-4afe-888a-d961b0717c7d.png">

Search for 61 popad and put the breakpoint on very next JMP instruction.

<img width="752" alt="Picture8" src="https://user-images.githubusercontent.com/107531426/178292094-b1fd6b6e-1328-432f-9803-6476e258a699.png">

Hit Enter to JMP. It will take you a place Hit F9 again. Run the sample until you get JMP breakpoint.

<img width="752" alt="Picture9" src="https://user-images.githubusercontent.com/107531426/178292423-fc2cad82-b35e-489b-9481-482b6669792b.png">
Do step over (F7). You can see your entrypoint and first byte of unpacked malware. 
(1CFE & 52,6A,36,68)
<img width="752" alt="Picture10" src="https://user-images.githubusercontent.com/107531426/178292611-4e46a65c-8057-4aa9-9a24-e1562c36650c.png">

 # 2. ESP Method
 Run the sample and do step over. You’ll see Entrypoint at ESP in Registers section. Right click to that address and do “follow in dump”
 
<img width="585" alt="dts" src="https://user-images.githubusercontent.com/107531426/178295205-e488dc46-d4f5-476c-961e-bf593a424cff.PNG">

Do BreakPoint>Hardware Access>Dword at the Dword (4Bytes) in Dump. 

<img width="586" alt="dts2" src="https://user-images.githubusercontent.com/107531426/178295943-29a10755-6484-4ed8-bfbe-bbd2da4a35f8.PNG">

Then Run the Sample. Hit the very next JMP. 

<img width="576" alt="dta" src="https://user-images.githubusercontent.com/107531426/178296617-f6110dfe-b04c-45d9-b9d0-0c9869eff89e.PNG">
You’ll be at Entrypoint of your unpacked Malware (1CFE & 52,6A,36,68)
<img width="572" alt="dtrr" src="https://user-images.githubusercontent.com/107531426/178297115-ca61975a-13e2-49c3-80a1-cb94030a9e8f.PNG">

# Now Importing Unpacked Malware    
Use Scylla plugin in x32dbg for this. Check IAT info, you’ll see your OEP. Click IAT autosearch
<img width="709" alt="Picture15" src="https://user-images.githubusercontent.com/107531426/178299308-410e74ce-b589-4474-bdae-e51db974c082.png">

Then click on Get Imports for imports  then Dump and save your unpacked binary.

<img width="711" alt="Picture16" src="https://user-images.githubusercontent.com/107531426/178299562-627d7b05-9f9c-41e3-8a6c-8b4bbe08382c.png">

<img width="485" alt="fgf" src="https://user-images.githubusercontent.com/107531426/178300168-87586941-b7bc-42e7-9a7f-44ec369fc917.PNG">




