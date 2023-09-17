# 文件批量解密
```python
import os
def decryption(path):
    with open(path, 'r+b') as f:
        content = f.read()
        index = content.count(b'UnityFS')
        if index == 2:
            first_pos = content.find(b'UnityFS')
            second_pos = content.find(b'UnityFS', first_pos + 1)
            content = content[second_pos:]
            f.seek(0)
            f.write(content)
            f.truncate()
            print("保存", path)
            return True
        else:
            print("跳过", path)
            return False

rootdir = r'\少女回战\files\_assets' # 改为你的路径
total_files = sum([len(files) for _, _, files in os.walk(rootdir)])
processed_files = 0
success_files = 0

for subdir, dirs, files in os.walk(rootdir):
    for file in files:
        path = os.path.join(subdir, file)
        if decryption(path):
            success_files += 1
        processed_files += 1
        progress = processed_files / total_files * 100
        print(
            f"已处理 {processed_files} / {total_files} 个文件，进度：{progress:.2f}% , 解密数量{success_files}")
```

# 音频提取
1. 音频路径 : 少女回战\拆包\assets\assets\sound\Android
2. 提取方法 : 使用RavioliGameTools导出为WEB和BNK文件为WEM文件,再使用vgmstream批量提出为WAV
3. 至于提取后怎么区分是哪个角色的...我也不知道,所以批量生成的这些模型我都没有设置触发配音

# 模型使用方法
使用Live2DViewerEX的编辑模型模式,直接打开Live2DViewerEX.config,打包为lpk上传到创意工坊
