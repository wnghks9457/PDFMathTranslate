<div align="center">

English | [简体中文](README_zh-CN.md)

<img src="./docs/images/banner.png" width="320px"  alt="PDF2ZH"/>  

<h2 id="title">PDFMathTranslate</h2>

<p>
  <!-- PyPI -->
  <a href="https://pypi.org/project/pdf2zh/">
    <img src="https://img.shields.io/pypi/v/pdf2zh"/></a>
  <a href="https://pepy.tech/projects/pdf2zh">
    <img src="https://static.pepy.tech/badge/pdf2zh"></a>
  <!-- License -->
  <a href="./LICENSE">
    <img src="https://img.shields.io/github/license/Byaidu/PDFMathTranslate"/></a>
  <a href="https://t.me/+Z9_SgnxmsmA5NzBl">
    <img src="https://img.shields.io/badge/Telegram-2CA5E0?style=flat-squeare&logo=telegram&logoColor=white"/></a>
</p>

</div>

PDF scientific paper translation and bilingual comparison.

- 📊 Preserve formulas, charts, table of contents, and annotations *([preview](#preview))*.
- 🌐 Support [multiple languages](#language), and diverse [translation services](#services).
- 🤖 Provides [commandline tool](#usage), [interactive user interface](#gui), and [Docker](#docker)

Feel free to provide feedback in [GitHub Issues](https://github.com/Byaidu/PDFMathTranslate/issues) or [Telegram Group](https://t.me/+Z9_SgnxmsmA5NzBl).

<h2 id="updates">Updates</h2>

- [Nov. 20 2024] Supports [Docker](#docker)  
- [Nov. 20 2024] Supports [multiple-threads translation](#threads)
- [Nov. 19 2024] Provides an [interactive graphical user interface](#gui)
- [Nov. 18 2024] Supports [more services: DeepL, DeepLX, and Azure](#services)

<h2 id="install">Installation</h2>

Require Python version >=3.8, <=3.12

```bash
pip install pdf2zh
```

<h2 id="usage">Usage</h2>

Execute the translation command in the command line to generate the translated document `example-zh.pdf` and the bilingual document `example-dual.pdf` in the current directory. Use Google as the default translation service.

<img src="./docs/images/cmd.explained.png" width="580px"  alt="cmd"/>  

Please refer to [ChatGPT](https://chatgpt.com/share/6734a83d-9d48-800e-8a46-f57ca6e8bcb4) for how to set environment variables.

<h2 id="partial">Full / partial document translation</h3>

- Entire document

  ```bash
  pdf2zh example.pdf
  ```

- Part of the document

  ```bash
  pdf2zh example.pdf -p 1-3,5
  ```

<h3 id="language">Specify source and target languages</h3>

See [Google Languages Codes](https://developers.google.com/admin-sdk/directory/v1/languages), [DeepL Languages Codes](https://developers.deepl.com/docs/resources/supported-languages)

```bash
pdf2zh example.pdf -li en -lo ja
```

<h3 id="services">Translate with Different Services</h3>

- **DeepL**

  See [DeepL](https://support.deepl.com/hc/en-us/articles/360020695820-API-Key-for-DeepL-s-API)

  Set ENVs to construct an endpoint like: `{DEEPL_SERVER_URL}/translate`
  - `DEEPL_SERVER_URL` (Optional), e.g., `export DEEPL_SERVER_URL=https://api.deepl.com`
  - `DEEPL_AUTH_KEY`, e.g., `export DEEPL_AUTH_KEY=xxx`

  ```bash
  pdf2zh example.pdf -s deepl
  ```

- **DeepLX**

  See [DeepLX](https://github.com/OwO-Network/DeepLX)

  Set ENVs to construct an endpoint like: `{DEEPL_SERVER_URL}/translate`
  - `DEEPLX_SERVER_URL` (Optional), e.g., `export DEEPLX_SERVER_URL=https://api.deeplx.org`
  - `DEEPLX_AUTH_KEY`, e.g., `export DEEPLX_AUTH_KEY=xxx`

  ```bash
  pdf2zh example.pdf -s deeplx
  ```

- **Ollama**

  See [Ollama](https://github.com/ollama/ollama)

  Set ENVs to construct an endpoint like: `{OLLAMA_HOST}/api/chat`
  - `OLLAMA_HOST` (Optional), e.g., `export OLLAMA_HOST=https://localhost:11434`

  ```bash
  pdf2zh example.pdf -s ollama:gemma2
  ```

- **LLM with OpenAI compatible schemas (OpenAI / SiliconCloud / Zhipu)**

  See [SiliconCloud](https://docs.siliconflow.cn/quickstart), [Zhipu](https://open.bigmodel.cn/dev/api/thirdparty-frame/openai-sdk)

  Set ENVs to construct an endpoint like: `{OPENAI_BASE_URL}/chat/completions`
  - `OPENAI_BASE_URL` (Optional), e.g., `export OPENAI_BASE_URL=https://api.openai.com/v1`
  - `OPENAI_API_KEY`, e.g., `export OPENAI_API_KEY=xxx`

  ```bash
  pdf2zh example.pdf -s openai:gpt-4o
  ```

- **Azure**

  See [Azure Text Translation](https://docs.azure.cn/en-us/ai-services/translator/text-translation-overview)

  Following ENVs are required:
  - `AZURE_APIKEY`, e.g., `export AZURE_APIKEY=xxx`
  - `AZURE_ENDPOINT`, e.g, `export AZURE_ENDPOINT=https://api.translator.azure.cn/`
  - `AZURE_REGION`, e.g., `export AZURE_REGION=chinaeast2`

  ```bash
  pdf2zh example.pdf -s azure
  ```

<h3 id="exceptions">Translate wih exceptions</h3>

Use regex to specify formula fonts and characters that need to be preserved.

```bash
pdf2zh example.pdf -f "(CM[^RT].*|MS.*|.*Ital)" -c "(\(|\||\)|\+|=|\d|[\u0080-\ufaff])"
```

<h3 id="threads">Specify threads</h3>

Use `-t` to specify how many threads to use in translation:

```bash
pdf2zh example.pdf -t 1
```

<h3 id="gui">Interact with GUI</h3>

<img src="./docs/images/before.png" width="500"/>

```bash
pdf2zh -i
```

See [documentation for GUI](./docs/README_GUI.md) for more details.

<h3 id="docker">Docker</h3>

1. Pull and run:

    ```bash
    docker pull byaidu/pdf2zh
    docker run -p 7860:7860 byaidu/pdf2zh
    ```

2. Open in browser:

    ```
    http://localhost:7860/
    ```

<h2 id="preview">Preview</h2>

![image](https://github.com/user-attachments/assets/57e1cde6-c647-4af8-8f8f-587a40050dde)

![image](https://github.com/user-attachments/assets/0e6d7e44-18cd-443a-8a84-db99edf2c268)

![image](https://github.com/user-attachments/assets/5fe6af83-2f5b-47b1-9dd1-4aee6bc409de)

<h2 id="acknowledgement">Acknowledgements</h2>

- Document merging: [PyMuPDF](https://github.com/pymupdf/PyMuPDF)

- Document parsing: [Pdfminer.six](https://github.com/pdfminer/pdfminer.six)

- Document extraction: [MinerU](https://github.com/opendatalab/MinerU)

- Multi-threaded translation: [MathTranslate](https://github.com/SUSYUSTC/MathTranslate)

- Layout parsing: [DocLayout-YOLO](https://github.com/opendatalab/DocLayout-YOLO)

- Document standard: [PDF Explained](https://zxyle.github.io/PDF-Explained/), [PDF Cheat Sheets](https://pdfa.org/resource/pdf-cheat-sheets/)

<h2 id="contrib">Contributors</h2>

<a href="https://github.com/Byaidu/PDFMathTranslate/graphs/contributors">
  <img src="https://opencollective.com/PDFMathTranslate/contributors.svg?width=890&button=false" />
</a>

<h2 id="star_hist">Star History</h2>

<a href="https://star-history.com/#Byaidu/PDFMathTranslate&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=Byaidu/PDFMathTranslate&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=Byaidu/PDFMathTranslate&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=Byaidu/PDFMathTranslate&type=Date" />
 </picture>
</a>
