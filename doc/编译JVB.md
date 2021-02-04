# 编译JVB

~~~shell
#JVB_HOME="The path to your JVB clone."

mvn package -DskipTests -Dassembly.skipAssembly=false

~~~



# RUN JVB

~~~shell
#解压
unzip jitsi-videobridge-2.1-SNAPSHOT

#创建配置文件
mkdir -p ~/.sip-communicator
cat > ~/.sip-communicator/sip-communicator.properties << EOF
org.jitsi.impl.neomedia.transform.srtp.SRTPCryptoContext.checkReplay=false
# The videobridge uses 443 by default with 4443 as a fallback, but since we're already
# running nginx on 443 in this example doc, we specify 4443 manually to avoid a race condition
org.jitsi.videobridge.TCP_HARVESTER_PORT=4443
EOF
#执行 --secret prosody配置文件中的密码
cd jitsi/jitsi-videobridge-2.1-SNAPSHOT/ && nohup ./jvb.sh --host=localhost --domain=jitsi.example.org --port=5347 --secret=IfGaish6 --apis=rest > ~/jvb.log
~~~



# 