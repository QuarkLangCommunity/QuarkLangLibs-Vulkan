# QuarkLangLibs-Vulkan

**QuarkLang 官方库（vulkan）——Vulkan 图形 API 绑定，官方认证。**

`vulkan.qk` 通过语言级 **`library` 系统库绑定**直接声明 Vulkan 导出符号，
运行时跨系统加载（Linux `libvulkan.so.1` / macOS `libvulkan.dylib` / Windows `vulkan-1.dll`）
并经 **libffi** 调用。

## 使用方法

```qk
import "vulkan";

fn main(io IOStream) {
    // 实例创建：pCreateInfo / pInstance 为句柄字符串（v1 十六进制句柄）
    code int = vulkan.vkCreateInstance("", "", "");
    io.println(code == vk::SUCCESS() || code >= vk::SUCCESS());
    io.println(vk::ERROR_OUT_OF_DATE_KHR());
}
```

## 声明集 API（常用面）

- 实例：`vkCreateInstance` / `vkDestroyInstance` / `vkEnumerateInstanceExtensionProperties` / `vkEnumerateInstanceLayerProperties`
- 物理设备：`vkEnumeratePhysicalDevices` / `vkGetPhysicalDeviceProperties` / `vkGetPhysicalDeviceFeatures` / `vkGetPhysicalDeviceQueueFamilyProperties` / `vkEnumerateDeviceExtensionProperties`
- 逻辑设备/队列：`vkCreateDevice` / `vkDestroyDevice` / `vkGetDeviceQueue` / `vkDeviceWaitIdle`
- 交换链/渲染：`vkCreateSwapchainKHR` / `vkAcquireNextImageKHR` / `vkQueueSubmit` / `vkQueuePresentKHR`
- 内存/缓冲：`vkAllocateMemory` / `vkFreeMemory` / `vkMapMemory` / `vkCreateBuffer` / `vkCreateImageView`
- 查询：`vkGetInstanceProcAddr`

常量判定在 `vk::` 空间：`vk::SUCCESS()` / `vk::ERROR_OUT_OF_DATE_KHR()` 等。

## 认证信息

- 库名：`vulkan`（`import "vulkan"`）—— `library vulkan` 声明 + `vk` 常量空间
- 语言版本：QuarkLang v0.2（`library` FFI / `space` / 泛型体系）
- 运行时版本：见主仓库 `engineVersion`
- 认证方：QuarkLang 官方项目

> 说明：`vulkan.qk` 是**声明集（认证）**——实际调用由运行时 FFI 完成；
> 窗口/表面（VkSurfaceKHR）由宿主负责，本库只管 Vulkan 调用面。
