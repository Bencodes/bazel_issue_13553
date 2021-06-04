Repro steps for https://github.com/bazelbuild/bazel/issues/13553

Running `bazel build //...` will produce the following exception:

```console
ERROR: /home/runner/.cache/bazel/_bazel_runner/5fed11dd6f3a570b9fabef4364fd1c6e/external/maven/BUILD:57:11: Desugaring v1/https/repo1.maven.org/maven2/org/jetbrains/kotlinx/kotlinx-coroutines-core-jvm/1.5.0/kotlinx-coroutines-core-jvm-1.5.0.jar for Android failed: (Exit 1): desugar_java8 failed: error executing command bazel-out/k8-opt-exec-2B5CBBC6/bin/external/bazel_tools/tools/android/desugar_java8 ... (remaining 1 argument(s) skipped)
java.lang.TypeNotPresentException: Type sun.misc.SignalHandler not present
	at java.base/sun.invoke.util.BytecodeDescriptor.parseSig(BytecodeDescriptor.java:97)
	at java.base/sun.invoke.util.BytecodeDescriptor.parseMethod(BytecodeDescriptor.java:69)
	at java.base/sun.invoke.util.BytecodeDescriptor.parseMethod(BytecodeDescriptor.java:45)
	at java.base/java.lang.invoke.MethodType.fromDescriptor(MethodType.java:1134)
	at java.base/java.lang.invoke.MethodType.fromMethodDescriptorString(MethodType.java:1113)
	at com.google.devtools.build.android.desugar.LambdaDesugaring$InvokedynamicRewriter.visitInvokeDynamicInsn(LambdaDesugaring.java:406)
	at org.objectweb.asm.MethodVisitor.visitInvokeDynamicInsn(MethodVisitor.java:461)
	at org.objectweb.asm.MethodVisitor.visitInvokeDynamicInsn(MethodVisitor.java:461)
	at com.google.devtools.build.android.desugar.strconcat.IndyStringConcatDesugaring$IndifiedStringConcatInvocationConverter.visitInvokeDynamicInsn(IndyStringConcatDesugaring.java:141)
	at org.objectweb.asm.MethodVisitor.visitInvokeDynamicInsn(MethodVisitor.java:461)
	at org.objectweb.asm.ClassReader.readCode(ClassReader.java:2444)
	at org.objectweb.asm.ClassReader.readMethod(ClassReader.java:1487)
	at org.objectweb.asm.ClassReader.accept(ClassReader.java:717)
	at com.google.devtools.build.android.desugar.Desugar.desugarClassesInInput(Desugar.java:544)
	at com.google.devtools.build.android.desugar.Desugar.desugarOneInput(Desugar.java:320)
	at com.google.devtools.build.android.desugar.Desugar.desugar(Desugar.java:240)
	at com.google.devtools.build.android.desugar.Desugar.processRequest(Desugar.java:1014)
	at com.google.devtools.build.android.desugar.Desugar.runPersistentWorker(Desugar.java:974)
	at com.google.devtools.build.android.desugar.Desugar.main(Desugar.java:952)
Caused by: java.lang.ClassNotFoundException: Class sun.misc.SignalHandler not found
	at com.google.devtools.build.android.desugar.io.HeaderClassLoader.findClass(HeaderClassLoader.java:53)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:588)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:521)
	at java.base/sun.invoke.util.BytecodeDescriptor.parseSig(BytecodeDescriptor.java:95)
	... 18 more
Target //:bazel_desugar_issue_13553 failed to build
```
