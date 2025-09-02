> [https://developer.nvidia.com/cuda-12-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=runfile_local](url) 

在英伟达官网选择服务器是配版本的CUDA Toolkits，这里选择wegt命令无需root权限
`wget https://developer.download.nvidia.com/compute/cuda/12.8.0/local_installers/cuda_12.8.0_570.86.10_linux.run`
（我的PyTorch 绑定的 CUDA 版本为12.8，所以这里的CUDA Toolkits选择的是12.8.0的版本）

可以在服务器中运行
`uname -a` 来查看自己的服务器详情

> 具体的安装教程可见csdn  [https://blog.csdn.net/dongbidsaxue/article/details/136633225?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522560a3eff92d49e06071d373a7f802f74%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=560a3eff92d49e06071d373a7f802f74&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-1-136633225-null-null.142^v102^pc_search_result_base8&utm_term=nvidia-cuda-toolkit%E5%AE%89%E8%A3%85&spm=1018.2226.3001.4187](url)



