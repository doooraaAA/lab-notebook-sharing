# 1. Pytorch 加速下载
```bash
pip3 install torch torchvision --index-url https://mirrors.nju.edu.cn/pytorch/whl/cu138
```
# 2. Jupyter 自动输出变量设置
> [!tip] Tips
> Jupyter 会默认显示最后一行的变量或者输出结果

## 方法一：使用以下代码，代码单元格中的所有单独变量都会自动显示，无需使用 `print`
```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```

>[!example] 举个栗子
>```python
>import torch
>x = torch.tensor([1.0, 2.0, 3.0])
>x
>```
>output:
>```python
>tensor([1., 2., 3.])
>```

##  方法二：使用 `display()` 函数（推荐）

`display()` 是 IPython 提供的专用函数，比 `print` 更强大，能利用 Jupyter 的丰富展示能力（如 HTML、图片、视频等）。
```python
from IPython.display import display
df1 = pd.DataFrame({'A': [1, 2]})
df2 = pd.DataFrame({'B': [3, 4]})
# 可以在任何位置，用`display()`输出多个对象
display(df1)
display(df2)
```
# 3. 最新Codex 解决手机号验证码方案-亲测有效
https://blog.csdn.net/Jack_num1/article/details/161649557
# 4. Quicker 效率工具，一键运行自定义动作
Quicker是Windows平台上一款“快捷面板+自动化引擎+启动器”三合一的效率神器。它通过鼠标中键呼出自定义快捷面板，将常用软件、高频操作甚至多步自动化流程整合为可视化按钮，一键即可完成过去需要多步操作的复杂任务。Quicker内置超过8000个用户共享的动作库，涵盖OCR识别、翻译、批量文件处理等场景，开箱即用。它还能根据当前使用的软件自动切换面板内容，真正做到“操作更少，收获更多”。

# 5. 踩坑总结：Jupyter中DataLoader多进程卡死

**问题现象**  
在Windows下的Jupyter Notebook训练MNIST，`DataLoader`设置`num_workers=2`，训练循环执行后内核卡死无响应，而同样的`.py`脚本却能正常运行。

**根本原因**  
- Windows多进程默认使用`spawn`方式启动子进程，子进程会**重新导入主模块**并执行所有全局代码。  
- Jupyter Notebook没有`if __name__ == '__main__'`保护机制（其`__name__`恒为`'__main__'`），导致子进程导入时**再次调用`get_mnist_loaders`创建DataLoader**，不断递归创建子进程，最终死锁。

**解决方案**  
将`num_workers`设为`0`，禁用多进程加载。MNIST数据量小，速度几乎不受影响，兼容性最好。

**经验教训**  
- 在Notebook中尽量使用`num_workers=0`，避免多进程兼容问题。  
- 大规模训练建议转成`.py`脚本，并用`if __name__ == '__main__'`保护主入口。  
- 遇到卡死先尝试`num_workers=0`，快速定位问题。  
- 不同环境（交互式 vs 脚本）的执行模型差异需格外注意，多进程代码务必考虑平台特性。
# 6. chatgpt充值
https://yingtu.ai/zh/blog/google-pay-apple-pay-link-subscribe-chatgpt-plus