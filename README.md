# CCTV 카메라 녹화 프로그램
## 프로젝트 설명
- CCTV 카메라를 제어하는 프로그램의 카메라 녹화 기능을 구현했습니다. 라즈베리파이 환경에서 동작했으며, c#과 VLC를 이용하였습니다. c#프로그램 내에서 VLC를 동작시켜 녹화를 진행하였습니다. config 입력값에 따라 녹화 진행 여부, 저장할 파일 경로 등이 결정되며, 하드 디스크의 용량을 체크하여 녹화파일이 저장되고, 하드디스크 용량이 부족한 경우 오래된 파일부터 삭제 처리하여 최신 녹화 영상이 남아있도록 기능을 구현했습니다.

> 이미지가 없어 가능 코드로 대체합니다.

### 프로그램 내 VLC 실행코드
```c#
sPath = "cvlc -vvv rtsp://"+sId+":"+sPw+"@"+sUrl+":"+sPort+"/Streaming/Channels/"+sPtzChannel+" --sout file/ps:"+Cam.sRecodingPath+"/"
								+DateTime.Now.ToString("yyyy-MM-dd-HH-mm-ss")+".h264 --stop-time="+Cam.sRecodingTime+" vlc://quit";

Util.Log.LogWrite(0, "SYS", "Run : ", "Recoding");

ProcessStartInfo psi = new ProcessStartInfo();
psi.FileName = "cvlc";
psi.Arguments = sPath;

psi.RedirectStandardOutput =true;
psi.UseShellExecute = false;

pRecordProcess = Process.Start(psi);

sRecordResult = pRecordProcess.StandardOutput.ReadLine();
pRecordProcess.WaitForExit();

pRecordProcess.Close();
```
### Config 정보
```c#
<add key="RECORDING" value="Y"/>
<add key="RECORDING_PATH" value="/share/recoding"/>
<add key="RECORDING_TIME" value="3600"/>
<add key="SAVE_DRIVE" value="/"/>
```
