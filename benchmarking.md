# Instructions

In order to run the benchmarks it is necessary to copy the correct files to the zedboard.

Currently we leverage the build scripts from the BBB target, 
thus we want to copy, to the zedboard, the binaries generated at:

```
scp -r <tf-root>/tensorflow/lite/tools/make/gen/bbb_armv7l  <username>@10.42.0.196:~/.
```

And the models available at `https://github.com/tflite-soc/tensorflow-models/tree/master/`

```
scp -r <models-folder> <username>@10.42.0.196:~/tensorflow-models/.
```

In order to run:
```
ssh <username>@10.42.0.196
cd bbb_armv7l/bin/
./benchmark_model --use_gpu=false --graph=../../tensorflow-models/mobilenet-v1/mobilenet_v1_1.0_224_quant.tflite
```

These steps will output:

```
root@localhost:~/bbb_armv7l/bin$ ./benchmark_model --use_gpu=false --graph=../../tensorflow-models/mobilenet-v1/mobilenet_v1_1.0_224_quant.tflite 
STARTING!
Min num runs: [50]
Min runs duration (seconds): [1]
Max runs duration (seconds): [150]
Inter-run delay (seconds): [-1]
Num threads: [1]
Benchmark name: []
Output prefix: []
Min warmup runs: [1]
Min warmup runs duration (seconds): [0.5]
Graph: [../../tensorflow-models/mobilenet-v1/mobilenet_v1_1.0_224_quant.tflite]
Input layers: []
Input shapes: []
Use gpu : [0]
Allow fp16 : [0]
Require full delegation : [0]
Enable op profiling: [0]
Max profiling buffer entries: [1024]
Loaded model ../../tensorflow-models/mobilenet-v1/mobilenet_v1_1.0_224_quant.tflite
resolved reporter
Initialized session in 21.039ms
Running benchmark for at least 1 iterations and at least 0.5 seconds but terminate if exceeding 150 seconds.
count=1 curr=751932

Running benchmark for at least 50 iterations and at least 1 seconds but terminate if exceeding 150 seconds.
count=50 first=747738 curr=747428 min=747331 max=748577 avg=747733 std=293

Average inference timings in us: Warmup: 751932, Init: 21039, no stats: 747733
```
