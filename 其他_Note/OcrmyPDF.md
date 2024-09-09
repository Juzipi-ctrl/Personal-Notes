## 基本示例[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#basic-examples)

### 帮助！[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#help)

OcrmyPDF有内置的帮助。

```
ocrmypdf --help
```

### 添加 OCR 图层并转换为 PDF/A[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#add-an-ocr-layer-and-convert-to-pdf-a)

```
ocrmypdf input.pdf output.pdf
```

### 添加 OCR 图层并输出标准 PDF[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#add-an-ocr-layer-and-output-a-standard-pdf)

```
ocrmypdf --output-type pdf input.pdf output.pdf
```

### 创建 PDF/A，将所有彩色和灰度图像转换为 JPEG[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#create-a-pdf-a-with-all-color-and-grayscale-images-converted-to-jpeg)

```
ocrmypdf --output-type pdfa --pdfa-image-compression jpeg input.pdf output.pdf
```

### 就地修改文件[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#modify-a-file-in-place)

仅当 OCRmyPDF 成功时，才会覆盖该文件。

```
ocrmypdf myfile.pdf myfile.pdf
```

### 正确的页面旋转[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#correct-page-rotation)

OCR 将尝试自动更正每个页面的旋转。这 可以帮助修复包含横向和混合的扫描作业 肖像页面。

```
ocrmypdf --rotate-pages myfile.pdf myfile.pdf
```

您可以增加（减少）参数以使页面旋转更（更少）激进。阈值数是比率 OCR 引擎对应更改文档图像的信心如何， 与保持不变相比。默认值非常保守;在某些文件上 它可能不会尝试旋转，除非它非常确信当前的 旋转是错误的。较低的值将产生更多的旋转，并且 更多误报。运行方式以查看每个的置信度 页面以查看您的文件是否有更好的价值。`--rotate-pages-threshold``2.0``-v1`

如果页面“只是水平有点偏离”，就像一张歪歪扭扭的图片， 那么你 want.is 红衣主教 角度是错误的。`--deskew``--rotate-pages`

### 英语以外的 OCR 语言[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#ocr-languages-other-than-english)

OCRmyPDF 假定文档是英文的，除非另有说明。光学字符识别 如果使用了错误的语言，质量可能会很差。

```
ocrmypdf -l fra LeParisien.pdf LeParisien.pdf
ocrmypdf -l eng+fra Bilingual-English-French.pdf Bilingual-English-French.pdf

ocrmypdf --output-type pdf --redo-ocr -l chi_sim+eng "被转换的文件名"
```

必须为所有指定的语言安装语言包。请参阅[安装其他语言包](https://ocrmypdf.readthedocs.io/en/latest/languages.html#lang-packs)。

不幸的是，Tesseract OCR 引擎无法检测 未知时的语言。

### 生成包含 OCR 文本的 PDF 和文本文件[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#produce-pdf-and-text-file-containing-ocr-text)

这将生成一个名为“output.pdf”的文件和一个名为 “输出.txt”。

```
ocrmypdf --sidecar output.txt input.pdf output.pdf
```

注意

挎斗文件包含由 OCRmyPDF 找到的**OCR 文本**。如果文档 包含已包含文本的页面，该文本不会出现在 边车。如果使用此选项，则仅使用OCR的那些页面 已执行将包含在边车中。如果跳过了某些页面 由于选项喜欢，那些页面 不会在边车里。`--pages``--skip-big``--tesseract-timeout`

如果您不想生成输出的 PDF，请使用 避免生成一个。将输出文件名设置为（即重定向到标准输出）。`--output-type=none``-`

要从 PDF 中提取所有文本，无论是从 OCR 还是其他方式生成， 使用像Poppler'sor这样的程序。`pdftotext``pdfgrep`

### OCR 图像，而不是 PDF[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#ocr-images-not-pdfs)

#### 选项：使用镶嵌[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#option-use-tesseract)

如果你从图像开始，你可以直接使用Tesseract来 将图像转换为 PDF：

```
tesseract my-image.jpg output-prefix pdf
# When there are multiple images
tesseract text-file-containing-list-of-image-filenames.txt output-prefix pdf
```

Tesseract的PDF输出非常好 - OCRmyPDF在内部使用它，在 有些情况。但是，OCRmyPDF 具有许多在 像图像处理、元数据控制和 PDF/A 生成一样。

#### 选项：使用 img2pdf[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#option-use-img2pdf)

您也可以使用[img2pdf](https://gitlab.mister-muffin.de/josch/img2pdf)之类的程序进行转换 您的图像到 PDF，然后通过管道将结果传送到运行 ocrmyPDF。告诉 ocrmypdf 读取标准输入。`-`

```
img2pdf my-images*.jpg | ocrmypdf - myfile.pdf
```

`img2pdf`推荐，因为它在 生成 PDF 而不对图像进行转码。

#### 选项：使用 OCRmyPDF（仅限单张图像）[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#option-use-ocrmypdf-single-images-only)

为方便起见，OCRmyPDF 还可以在其上将单个图像转换为 PDF 有。如果未设置图像的分辨率（每英寸点数，DPI）或 不正确，可以覆盖它。（因为 1 英寸是 2.54 厘米，1 dpi = 0.39 dpcm）。`--image-dpi`

```
ocrmypdf --image-dpi 300 image.png myfile.pdf
```

如果您有多个图像，则必须使用 图像到 PDF。`img2pdf`

#### 不推荐[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#not-recommended)

我们警告不要使用ImageMagick或Ghostscript将图像转换为 PDF，因为它们可能会对图像进行转码或生成缩减采样的图像， 有时毫无征兆。

## 图像处理[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#image-processing)

OCRmyPDF 在 PDF 的每一页上执行一些图像处理，如果 期望。对每个页面应用相同的处理。建议 用户在图像处理后查看文件，如以下命令 可能会删除所需的内容，尤其是从质量较差的扫描中删除的内容。

- `--rotate-pages`尝试确定正确的方向 每个页面，并在必要时旋转页面。
- `--remove-background`尝试检测和消除干扰 灰度或彩色图像的背景。单色图像是 忽视。这不应用于包含颜色的文档 照片，因为它可能会删除它们。
- `--deskew`将更正页面以倾斜的角度扫描 将它们旋转回原位。
- `--clean`使用[解纸](https://www.flameeyes.eu/projects/unpaper)清理 页面，但不更改最终输出。这使得它 OCR 尝试在背景噪音中查找文本的可能性较小。
- `--clean-final`在 OCR 之前使用纸张清理页面，并且 将页面插入到最终输出中。您将需要查看每个 页面，以确保 Unpaper 没有删除重要内容。

注意

在许多情况下，图像处理会将PDF页面栅格化为图像， 可能会降低质量。

警告

```
--clean-final`并且可能会留下不良 某些图像中的视觉伪影，其算法具有 缺点。使用这些文件后应目视查看文件 选项。`--remove-background
```

### 示例：OCR 和正确的文档倾斜（歪斜扫描）[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#example-ocr-and-correct-document-skew-crooked-scan)

纠偏：

```
ocrmypdf --deskew input.pdf output.pdf
```

图像处理命令可以组合。选项的顺序 给予并不重要。OCRmyPDF 始终应用以下步骤 图像处理管道按相同顺序排列（旋转、删除背景、 纠偏，干净）。

```
ocrmypdf --deskew --clean --rotate-pages input.pdf output.pdf
```

## 实际上不要对我的 PDF 进行 OCR[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#don-t-actually-ocr-my-pdf)

如果您设置OCRmyPDF将应用其图像 在不执行OCR的情况下进行处理，如果您只想应用图像 处理或 PDF/A 转换。`--tesseract-timeout 0`

```
ocrmypdf --tesseract-timeout=0 --remove-background input.pdf output.pdf
```

### 在不执行 OCR 的情况下优化图像[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#optimize-images-without-performing-ocr)

您还可以在不执行任何 OCR 的情况下优化所有图像：

```
ocrmypdf --tesseract-timeout=0 --optimize 3 --skip-text input.pdf output.pdf
```

### Process only certain pages[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#process-only-certain-pages)

You can ask OCRmyPDF to only apply [image processing](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#image-processing) and OCR to certain pages.

```
ocrmypdf --pages 2,3,13-17 input.pdf output.pdf
```

Hyphens denote a range of pages and commas separate page numbers. If you prefer to use spaces, quote all of the page numbers: .`--pages '2, 3, 5, 7'`

OCRmyPDF will warn if your list of page numbers contains duplicates or overlap pages. OCRmyPDF does not currently account for document page numbers, such as an introduction section of a book that uses Roman numerals. It simply counts the number of virtual pieces of paper since the start.

Regardless of the argument to , OCRmyPDF will optimize all pages/images in the file and convert it to PDF/A, unless you disable those options. Both of these steps are “whole file” operations. In this example, we want to OCR only the title and otherwise change the PDF as little as possible:`--pages`

```
ocrmypdf --pages 1 --output-type pdf --optimize 0 input.pdf output.pdf
```

## Redo existing OCR[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#redo-existing-ocr)

To redo OCR on a file OCRed with other OCR software or a previous version of OCRmyPDF and/or Tesseract, you may use the argument. (Normally, OCRmyPDF will exit with an error if asked to modify a file with OCR.)`--redo-ocr`

This may be helpful for users who want to take advantage of accuracy improvements in Tesseract for files they previously OCRed with an earlier version of Tesseract and OCRmyPDF.

```
ocrmypdf --redo-ocr input.pdf output.pdf
```

此方法将在不栅格化的情况下替换 OCR，从而降低质量或 去除矢量内容。如果文件包含纯数字文本的混合 和 OCR，数字文本将被忽略，OCR 将被替换。因此 此模式与图像处理选项不兼容，因为它们 更改文件的外观。

在某些情况下，无法检测或替换现有的 OCR。文件 例如，由 OCRmyPDF v2.2 或更早版本生成的是内部的 表示为具有可见文本，顶部绘制了不透明图像。 无法检测到这种情况。

如果不起作用，您可以使用，这将 强制对所有页面进行光栅化，可能会降低质量或丢失 矢量内容。`--redo-ocr``--force-ocr`

## 提高 OCR 质量[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#improving-ocr-quality)

[图像处理](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#image-processing)功能可以提高 OCR 质量。

旋转页面和纠偏有助于确保页面方向 在 OCR 开始之前是正确的。去除背景和/或清洁 该页面还可以改善结果。论证可以 指定在尝试之前将图像重新采样为更高分辨率 光学字符识别;这也可以改善结果。`--oversample DPI`

如果输入图像的分辨率不正确，OCR 质量将受到影响 （因为将检查可能的字体的像素大小范围 也将不正确）。

## 文档优化[¶](https://ocrmypdf.readthedocs.io/en/latest/cookbook.html#pdf-optimization)

默认情况下，OCRmyPDF 将尝试对 OCR 完成后 PDF 中的图像。执行优化 即使找不到 OCR 文本。

（简写）参数控制优化， 其中范围从 0 到 3（含 0 和 3），类似于优化 GCC 编译器中的级别。`--optimize N``-O``N`

| 水平           | 评论                                                         |
| -------------- | ------------------------------------------------------------ |
| `--optimize 0` | 禁用优化。                                                   |
| `--optimize 1` | 启用无损优化，例如将图像转码为更多 高效的格式。同时压缩 PDF 并在 PDF 中启用更高效的“对象流”。 （发出 Ifis，然后使用有损 JBIG2 优化。 使用有损 JBIG2 的决定与标准优化是分开的 设置。`--jbig2-lossy` |
| `--optimize 2` | 以上所有，并实现有损优化和颜色量化。                         |
| `--optimize 3` | 所有这些，并实现更积极的优化并针对较低的图像质量。           |

当 JBIG2 编码器可用以及何时安装时，优化得到了改进。如果缺少这些组件中的任何一个， 则某些类型的图像无法优化。`pngquant`

可用的优化类型可能会随着时间的推移而扩展。默认情况下， OCRmyPDF 压缩 PDF 中的数据流，并将更改 低效的压缩模式到更现代的版本。类似程序可用于更改编码，例如检查内部 的 PDF。`qpdf`

```
ocrmypdf --optimize 3 in.pdf out.pdf  # Make it small
```

一些用户可能会考虑启用有损 JBIG2。参见：jbig2-lossy.

注意

图像处理和 PDF/A 转换也会引入有损转换 到您的 PDF 图像，即使在使用时也是如此。`--optimize 1`