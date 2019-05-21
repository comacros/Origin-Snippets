# Origin-Snippets

LabTalk, Python, Origin-C and HTML/JavaScript snippets to free you hands.


1. [LabTalk, Python and Origin-C](#labtalk-python-and-origin-c)
2. [HTML and JavaScript](#html-and-javascript)

## LabTalk, Python and Origin-C
1. [Stack Groups in Worksheet](#stack-groups-in-worksheet)
2. [Remove Links in Worksheet](#remove-links-in-worksheet)
3. [Pass Vector Values Between Origin C and C++](#pass-vector-values-between-origin-c-and-c)

### Stack Groups in Worksheet
LabTalk
```
int nGroups = 3;
int nFields = 3;
for(int i = 1; i <= nGroups; i++)
{
  for(int j = 1; j <= nFields; j++)
  {
    range src = [Book1]Sheet1!wcol((i-1)*nGroups+j);
    range dst = [Book2]Sheet1!wcol(j);
    copy -a src dst;
  }
}
```
<img src="Screenshots/Stack Columns in Single Worksheet.png">

### Remove Links in Worksheet
LabTalk
```
for(int i = 1; i <= wks.ncols; i++)
{
    range rr = !$(i);
    %A = [%H]%(wks.name$);
    dataset ds = %A!$(i);
    rr = ds;
}
```

### Pass Vector Values Between Origin C and C++
#### Pass vector values from Origin C to C++
C++
```
extern "C"
__declspec(dllexport)
void Foo(double* p, size_t n)
{
    std::vector<double> xs;
    xs.assign(p, p + n);
    
    // ...
    
    return;
}
```
Origin C
```
void Bar()
{
    vector<double> xs(1024);
    size_t n = xs.GetSize();
    Foo(xs, n);
    
    return;
}
```
#### Pass vector values from C++ to Origin C
C++
```
extern "C"
__declspec(dllexport)
void ReleaseMemory(void* p)
{
    if(p)
    {
        free(p);
        p = nullptr;
    }
}

extern "C"
__declspec(dllexport)
void Foo(double** p, size_t* n)
{
    std::vector<double> xs(1024);
    *n = xs.size();
    *p = (double*)calloc(xs.size(), sizeof(double));
    memcpy(*p, xs.data(), xs.size() * sizeof(double));
    
    return;
}
```
Origin C
```
void Bar()
{
    double* p;
    size_t n;
    Foo(&p, &n);
    
    vector<double> xs(n);
    if(n)
        memcpy(xs, p, n * sizeof(double));
    ReleaseMemory(p);
    
    return;
}
```

## HTML and JavaScript

1. [Center Alignment for an Image](#center-alignment-for-an-image)
2. [MathJax](#mathjax)

### Center Alignment for an Image
```
<img alt='{{graph://graph1}}' style='display:block; margin:0 auto;' width='300px'>
```

### MathJax
```
 <script type='text/x-mathjax-config'>
    MathJax.Hub.Config({
      extension: ["tex2jax.js", "TeX/AMSmath.js"],
      jax:["input/TeX", "output/SVG"],
      //displayAlign: "left"
    })
  </script>
  <script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=default">
</script>
<div>
  Inline equation: \(f\left(x\right)=a+bx\)
</div>
<div>
  Display:
  \[
  P\left(x\right)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\left(x-\mu\right)^2/2\sigma^2}
  \]
</div>
```
<img src="Screenshots/mathjax.png">
