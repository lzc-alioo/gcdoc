
java -agentlib:hprof=cpu=samples,interval=20,depth=3 -cp  javademo-1.0.0-SNAPSHOT-jar-with-dependencies.jar com.alioo.md5.Md5demo

```
CPU SAMPLES BEGIN (total = 1426) Fri Nov 15 03:17:06 2019
rank   self  accum   count trace method
   1 76.37% 76.37%    1089 300138 java.util.Random.next
   2  5.68% 82.05%      81 300144 com.alioo.md5.MD5Util.byteArrayToHexString
   3  3.65% 85.69%      52 300145 java.lang.StringCoding$StringEncoder.encode
   4  2.31% 88.01%      33 300206 java.lang.String.toUpperCase
   5  1.96% 89.97%      28 300205 sun.security.jca.GetInstance.getInstance
   6  1.68% 91.65%      24 300148 sun.security.jca.GetInstance.getInstance
   7  1.33% 92.99%      19 300146 sun.security.provider.MD5.implDigest
   8  0.98% 93.97%      14 300207 sun.security.provider.DigestBase.implCompressMultiBlock
   9  0.84% 94.81%      12 300210 sun.security.provider.MD5.implCompress
  10  0.63% 95.44%       9 300132 sun.reflect.Reflection.getCallerClass
  11  0.63% 96.07%       9 300143 com.alioo.md5.Md5demo.main
  12  0.49% 96.56%       7 300208 java.lang.Thread.sleep
  13  0.42% 96.98%       6 300118 sun.security.provider.MD5.implCompress
  14  0.35% 97.34%       5 300137 com.alioo.md5.Md5demo.main
  15  0.28% 97.62%       4 300136 com.alioo.md5.Md5demo.main
  16  0.28% 97.90%       4 300140 com.alioo.md5.Md5demo.main
  17  0.28% 98.18%       4 300209 com.alioo.md5.Md5demo.main
  18  0.21% 98.39%       3 300212 sun.security.provider.DigestBase.engineUpdate
  19  0.14% 98.53%       2 300076 java.lang.ClassLoader.findBootstrapClass
  20  0.14% 98.67%       2 300139 java.util.Arrays.copyOfRange
  21  0.14% 98.81%       2 300142 java.lang.AbstractStringBuilder.<init>
  22  0.14% 98.95%       2 300211 sun.security.jca.GetInstance.getInstance
  23  0.14% 99.09%       2 300213 sun.security.provider.MD5.implCompress
  24  0.14% 99.23%       2 300215 java.lang.String.getBytes
  25  0.14% 99.37%       2 300216 java.util.Arrays.copyOf
  26  0.07% 99.44%       1 300044 sun.util.calendar.ZoneInfoFile.load
  27  0.07% 99.51%       1 300133 java.security.Provider$Service.newInstance
  28  0.07% 99.58%       1 300134 java.lang.Object.clone
  29  0.07% 99.65%       1 300141 com.alioo.md5.Md5demo.main
  30  0.07% 99.72%       1 300147 java.lang.String.startsWith
  31  0.07% 99.79%       1 300214 java.lang.StringBuilder.toString
  32  0.07% 99.86%       1 300217 com.alioo.md5.Md5demo.getRandomStr
  33  0.07% 99.93%       1 300218 java.lang.StringBuilder.toString
  34  0.07% 100.00%       1 300219 java.lang.StringBuilder.toString
CPU SAMPLES END

```



