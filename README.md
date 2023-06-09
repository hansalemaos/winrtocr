# Multiprocessing library for OCR with WinRT  

## pip install winrtocr

### Tested against Windows 10 / Python 3.10 / Anaconda 

#### The results are not as good as the ones from Tesseract or EasyOCR, but it is way faster. 



```python

from winrtocr import WinRTocr
from time import perf_counter
from a_cv_imwrite_imread_plus import open_image_in_cv



winrto = WinRTocr(cpus=5, language="en-US")
picslinks = [
    r"https://github.com/hansalemaos/screenshots/raw/main/pandsnesteddicthtml.png",
    r"https://github.com/hansalemaos/screenshots/raw/main/cv2_putTrueTypeText_000000.png",
    r"https://github.com/hansalemaos/screenshots/raw/main/cv2_putTrueTypeText_000008.png",
    r"https://github.com/hansalemaos/screenshots/raw/main/cv2_putTrueTypeText_000017.png",
]

picsunique = [open_image_in_cv(x, channels_in_output=4) for x in picslinks]
pics = []
for _ in range(100):
    pics.extend(picsunique)

start = perf_counter()
dfa = winrto.get_ocr_df(pics)
print(f"Multi: {perf_counter()-start}")

dfa2 = winrto.get_ocr_df_and_pics(pics)
```
