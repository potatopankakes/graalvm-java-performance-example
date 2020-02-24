# GraalVM Example: GraalVM vs AdoptOpenJDK/JVM

This repository contains the code for the GraalVM demo at [https://www.graalvm.org/docs/examples/java-performance-examples/].

## Prerequisite Installations
* [asdf](https://github.com/asdf-vm)
* GraalVM plugin for `asdf` (`asdf plugin add graalvm`)
* Java plugin for `asdf` (`asdf plugin add java`)

## Preparation

* `Run `asdf install` to install the correct GraalVM (as well as, NodeJS and Java)
Download or clone this repository:
```
git clone git@github.com:potatopankakes/graalvm-java-performance-example.git
cd graalvm-java-performance-example
cd graalvm
asdf install
cd ../java11
asdf install
cd ../
```

## See Performance of AdoptOpenJDK/JVM

Verify that you are using AdoptOpenJDK and not GraalVM.  Also verify that the version is `11.0.6`.
```
cd java11
java -version
javac -version
```

Compile the performance test:
```
javac ../CountUppercase.java -d ./
```

Now run the performance test multiple times:
```
LMTC-JBURKE:java11 jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (362 ms)
2 (348 ms)
3 (249 ms)
4 (243 ms)
5 (251 ms)
6 (257 ms)
7 (250 ms)
8 (246 ms)
9 (246 ms)
total: 69999993 (2695 ms)
LMTC-JBURKE:java11 jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (314 ms)
2 (275 ms)
3 (181 ms)
4 (176 ms)
5 (173 ms)
6 (172 ms)
7 (173 ms)
8 (172 ms)
9 (173 ms)
total: 69999993 (1982 ms)
LMTC-JBURKE:java11 jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (361 ms)
2 (257 ms)
3 (178 ms)
4 (174 ms)
5 (174 ms)
6 (171 ms)
7 (173 ms)
8 (173 ms)
9 (173 ms)
total: 69999993 (2007 ms)
LMTC-JBURKE:java11 jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (282 ms)
2 (264 ms)
3 (177 ms)
4 (177 ms)
5 (178 ms)
6 (176 ms)
7 (174 ms)
8 (174 ms)
9 (173 ms)
total: 69999993 (1949 ms)
```

Notice how all these timings are generally never get below than 171-173ms using AdoptOpenJDK.


## See Performance of GraalVM

Verify that you are using OpenJDK GraalVM.  Also verify that the version is `11.0.6`.
```
cd ../graalvm  # if you are still in the `java11` subdirectory
java -version
javac -version
```

Compile the performance test:
```
javac ../CountUppercase.java -d ./
```

Now run the performance test multiple times:
```
LMTC-JBURKE:graalvm jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (236 ms)
2 (146 ms)
3 (76 ms)
4 (66 ms)
5 (66 ms)
6 (66 ms)
7 (64 ms)
8 (68 ms)
9 (66 ms)
total: 69999993 (918 ms)
LMTC-JBURKE:graalvm jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (293 ms)
2 (164 ms)
3 (84 ms)
4 (76 ms)
5 (73 ms)
6 (77 ms)
7 (63 ms)
8 (66 ms)
9 (65 ms)
total: 69999993 (1025 ms)
LMTC-JBURKE:graalvm jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (222 ms)
2 (139 ms)
3 (73 ms)
4 (65 ms)
5 (65 ms)
6 (66 ms)
7 (64 ms)
8 (110 ms)
9 (66 ms)
total: 69999993 (941 ms)
LMTC-JBURKE:graalvm jburke$ java CountUppercase In 2019 I would like to run ALL languages in one VM.
1 (226 ms)
2 (144 ms)
3 (87 ms)
4 (78 ms)
5 (74 ms)
6 (71 ms)
7 (70 ms)
8 (67 ms)
9 (66 ms)
total: 69999993 (948 ms)
```

Notice how all these timings are generally never get below than 63-66ms using GraalVM.

## Summary

In this computationally dominate example, depending on what timings are compared, GraalVM is approximately 2-3x faster.
