---
title: Find the NVIDIA GPU architecture
---
1. Go the the terminal and type `nvidia-smi`
2. The output will look like this:

```bash
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.xx.xx    Driver Version: 515.xx.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro P1000        Off  | 00000000:01:00.0  On |                  N/A |
| 34%   41C    P8    N/A /  N/A |    299MiB /  4096MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```
3. From the output, you can see that the GPU is **Quadro P1000**. Now, go to the [NVIDIA website](https://developer.nvidia.com/cuda-gpus) and find the GPU architecture. In this case, the GPU architecture is **Pascal**.

4. Also look for the **CUDA Capability**. In this case, the CUDA capability is **6.1**.

5. Therefore, for this GPU, the architecture is **Pascal** and the CUDA capability is **6.1**. And for pcms, you will write `PASCAL61`.

6. If you do not find the GPU listed in the NVIDIA website, then you can also use this wikipedia [page](https://en.wikipedia.org/wiki/CUDA#GPUs_supported) to find the GPU architecture.

