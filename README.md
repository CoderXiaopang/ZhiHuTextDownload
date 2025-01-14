# Zhihu Paid Column Font Decoder

本项目可自动抓取并解码知乎付费专栏中的自定义字体，以解决乱码问题，并最终生成可读的文本文件。

> **免责声明**：  
> 本项目仅供个人学习与研究使用，不得用于任何商业用途或违反知乎及相关平台的用户协议、服务条款及版权声明的行为。请自行承担可能产生的法律风险。

## 功能介绍

1. **自动获取页面内容**：通过传入知乎付费专栏 URL，脚本会自动抓取并解析页面，保存内容到本地。  
2. **自定义字体解析**：部分专栏使用自定义字体对文本进行混淆，通过 `fontTools` 结合 `ddddocr` 和 `modelscope` OCR 模型，还原混淆文本。  
3. **文本替换与修正**：程序根据识别的映射关系替换混淆字符，输出可阅读的纯文本文件。  
4. **多节爬取**：检测到下一节链接后，会依次自动获取后续章节，直至抓取完毕或无法找到下一节链接。

## 环境配置

本项目使用 `conda` 进行环境管理，提供了 `environment.yml` 文件，可快速创建所需环境并安装所有依赖。

1. 克隆或下载本项目：
   ```bash
   git clone https://github.com/your-username/zhihu-paid-column-font-decoder.git
   cd zhihu-paid-column-font-decoder
   ```
2. 创建并激活 conda 环境：
   ```bash
   conda env create -f environment.yml
   conda activate zhihu-font-decoder
   ```
   > 注意：上面命令中的环境名称需要与你的 `environment.yml` 文件中的 `name` 字段一致。  
3. 若后续需要更新依赖，可在项目目录下使用：
   ```bash
   conda env update -f environment.yml
   ```

## 使用方法

1. **准备知乎 Cookies**  
   - 在项目根目录下新建（或使用已有）文件 `ck.txt`，将知乎登录后的 Cookies 信息写入其中。
   - **注意**：Cookies 通常具有时效性，若失效需要重新获取。

2. **配置代码中的起始专栏链接**  
   - 在 `main.py`（或相应的主文件）中，找到
     ```python
     firstsession_url = "https://www.zhihu.com/market/paid_column/xxxx/section/xxxx"
     ```
     将其替换为你需要抓取的知乎付费专栏第一节文章的链接。

3. **运行脚本**  
   ```bash
   python main.py
   ```
   - 执行后会弹出一个文件夹选择对话框，选定文件夹用于保存抓取结果。  
   - 脚本会自动爬取和识别付费专栏内容，并将解码后的文本文件保存到你指定的目录中。  
   - 当检测到下一节链接时，会持续抓取下一节内容，直至无法检测到新的章节链接。

4. **查看结果**  
   - 所有章节将按照章节顺序生成文本文件，保存在你选择的文件夹中。  
   - 如果需要保存原始 HTML 文件，可在调用 `save_content` 方法时修改 `file_type` 参数为 `'html'`。

## 文件结构

```
zhihu-paid-column-font-decoder
├── ck.txt                  # 存储知乎 Cookies
├── main.py                 # 项目主入口（示例）
├── environment.yml         # conda 环境配置文件
└── README.md               # 使用说明
```

## 注意事项

1. **自定义字体识别准确度**  
   - 本项目使用 [ddddocr](https://github.com/sml2h3/ddddocr) 和 [modelscope OCR](https://github.com/modelscope/modelscope) 进行字符识别，若识别结果有误，可在代码中尝试调整参数或更换其他识别方法。
2. **合法合规抓取**  
   - 请务必遵守 [知乎用户协议](https://www.zhihu.com/terms) 和相关法律法规，确认仅限在合法授权的前提下获取专栏内容。  
   - 本项目仅供学习交流，因使用引起的任何责任需自行承担。
3. **Cookies 失效问题**  
   - `ck.txt` 内 Cookies 若失效，需要重新获取并替换，否则脚本无法正常爬取付费专栏。
4. **网络请求间隔**  
   - 默认在发送请求后有一定时间间隔（如 2 秒或 5 秒），防止过快访问导致 IP 被封或其他请求限制。可根据需要适度调整。

## 引用 & 致谢

- 部分思路及原始代码参考自 [CSDN - cc605523](https://blog.csdn.net/cc605523/article/details/140820570)，感谢分享。  
- 字体/文本识别相关依赖：
  - [ddddocr](https://github.com/sml2h3/ddddocr)  
  - [modelscope - Damo OCR](https://github.com/modelscope/modelscope)  
  - [fontTools](https://github.com/fonttools/fonttools)  

## 许可证

本项目内所使用的第三方依赖均遵循各自的开源协议（MIT、Apache-2.0 等），请自行查阅。项目本身可根据需求选择合适的开源协议（如 MIT、Apache-2.0、GPLv3 等），以下以 **MIT License** 为例：

```
MIT License

Copyright (c) 2023 ...

Permission is hereby granted, free of charge, to any person obtaining a copy ...
```

如有改进建议或 Bug 反馈，欢迎在项目的 [Issues](https://github.com/your-username/zhihu-paid-column-font-decoder/issues) 中提出。 祝使用愉快！
