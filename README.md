![Logo](https://ws2.sinaimg.cn/large/006tNc79ly1fl3joaz995j31kw09htj4.jpg)

<!--&middot;-->
[![Travis](https://img.shields.io/travis/stackhou/YJBannerViewOC.svg?style=flat)](https://github.com/stackhou/YJBannerViewOC.git)
[![Language](https://img.shields.io/badge/Language-Objective--C-FF7F24.svg?style=flat)](https://github.com/YJManager/YJBannerViewOC.git)
[![CocoaPods](https://img.shields.io/cocoapods/p/YJBannerView.svg)](https://github.com/stackhou/YJBannerViewOC.git)
[![CocoaPods](https://img.shields.io/cocoapods/v/YJBannerView.svg)](https://github.com/stackhou/YJBannerViewOC.git)
[![Carthage Compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/stackhou/YJBannerViewOC.git)
<!-- [![CocoaPods](https://img.shields.io/cocoapods/at/YJBannerView.svg)](https://github.com/stackhou/YJBannerViewOC.git) -->

# YJBannerView
- 使用简单、功能丰富的 `Objective-C版` 轮播控件,  基于 `UICollectionView` 实现, 多种场景均支持使用.

## 效果样例
<img src="https://github.com/stackhou/YJBannerViewOC/blob/master/YJBannerViewDemo/Resources/bannerDemo.gif" width="300" height="563" />

## Features

- [x] 支持自带PageControl样式配置, 也支持自定义        
- [x] 支持上、下、左、右四个方向自动、手动动滚动
- [x] 支持自动滚动时间设置                               
- [x] 支持首尾循环滚动的开关
- [x] 支持滚动相关手势的开关                             
- [x] 支持ContentMode的设置                            
- [x] 支持Banner标题的设置自定义
- [x] 支持自定义UICollectionViewCell                    
- [x] 支持自定义 UIView 填充BannerView
- [x] 支持在Storyboard\xib中创建并配置其属性   
- [x] 支持非首尾循环的Footer样式和进入详情回调
- [x] 不依赖其他三方SDWebImage或者AFNetworking设置图片
- [x] 支持CocoaPods
- [x] 支持Carthage
- [x] 支持获取当前位置的自身偏移量


## Installation

### Cocoapods

YJBannerView is available through [CocoaPods](http://cocoapods.org). To install it, simply add the following line to your Podfile:

```ruby
    pod 'YJBannerView'
```

### Carthage
```ruby
    github "stackhou/YJBannerViewOC"
```

## Usage

### 1.创建BannerView:
```objc
-(YJBannerView *)normalBannerView{
    if (!_normalBannerView) {
        _normalBannerView = [YJBannerView bannerViewWithFrame:CGRectMake(0, 20, kSCREEN_WIDTH, 180) dataSource:self delegate:self placeholderImageName:@"placeholder" selectorString:@"sd_setImageWithURL:placeholderImage:"];
        _normalBannerView.pageControlAliment = PageControlAlimentRight;
        _normalBannerView.autoDuration = 2.5f;
    }
    return _normalBannerView;
}
```
### 2.实现数据源方法和代理:
```objc
// 将网络图片或者本地图片 或者混合数组
- (NSArray *)bannerViewImages:(YJBannerView *)bannerView{
    return self.imageDataSources;
}

// 将标题对应数组传递给bannerView 如果不需要, 可以不实现该方法
- (NSArray *)bannerViewTitles:(YJBannerView *)bannerView{
    return self.titlesDataSources;
}

// 代理方法 点击了哪个bannerView 的 第几个元素
-(void)bannerView:(YJBannerView *)bannerView didSelectItemAtIndex:(NSInteger)index{
    NSString *title = [self.titlesDataSources objectAtIndex:index];
    NSLog(@"当前%@-->%@", bannerView, title);
}
```

### 扩展自定义方法
```objc
// 自定义Cell方法
- (Class)bannerViewCustomCellClass:(YJBannerView *)bannerView{
    return [HeadLinesCell class];
}

// 自定义Cell的数据刷新方法
- (void)bannerView:(YJBannerView *)bannerView customCell:(UICollectionViewCell *)customCell index:(NSInteger)index{

    HeadLinesCell *cell = (HeadLinesCell *)customCell;
    [cell cellWithHeadHotLineCellData:@"打折活动开始了~~快来抢购啊"];
}
```

## 版本记录

日期 | 版本号 | 更新内容
------ | ----- | ----
2015-5-10~2016-10-17 | 1.0~2.0 | 2.0之前的更新内容没有实际意义，省略...
2016-10-17~2017-01-01 | 2.0~2.1 | 功能完善Bug修复等
2017-01-01~2017-07-30 | 2.1~2.2 | 主要功能优化，新增FooterView等
2017-7-30~2017-09-30 |  2.2.0~2.3.0 | 调优、降低内存消耗等
2017-9-30 | 2.3.0 | 调优 创建该控件由原来的120毫秒 优化到只需要60毫秒左右，和创建一个UILabel相当。
2017-11-1 | 2.3.1 | 增加停止定时器和重新开启定时器API
2017-11-16 | 2.3.2 | 修复当数据为空时刷新后再次有数据刷新不滚动问题
2017-12-05 | 2.3.4 | 规范图片加载流程
2017-12-06 | 2.3.5 | 区分没有数据的占位图片和图片未加载的占位图片
2017-12-14 | 2.3.6 | 数据安全保护和数据更新速度优化
2017-12-15 | 2.3.7 | 增加当前滚动位置相对偏移量API

## 优化表现

- 简单设置时：

![](https://ws2.sinaimg.cn/large/006tKfTcly1fk1lk1i4d7j30c903uwf8.jpg)

- 复杂设置时:

![](https://ws2.sinaimg.cn/large/006tKfTcly1fk1lktrc6fj30bu03q750.jpg)

---
# 特殊需求

## 需求：
UI设计APP的 BannerView 轮播图的图片每个Item尺寸不同，比如：设计 BannerView 的可视区域大小是 375 x 420px, 而图片来源一些是375 x 420px, 而另一些是 375 x 450px 的, 对于高度为 450px 的图片就会有 y 方向上的压缩，造成变形。

## 解决办法：
将不同尺寸的图片资源用不同的控件放置，控件A放置 375 x 420px的图片，控件B放置 375 x 450 的图片，将这些控件放置在轮播组件上。Frame 分别设置成(0, 0, 375, 420) 和 (0, -30, 375, 450)。

## 代码
实现自定义View的代理方法即可传递不同尺寸的 View

```objc
- (UIView *)bannerView:(YJBannerView *)bannerView viewForItemAtIndex:(NSInteger)index{

    if (bannerView == self.customBannerView) {

        UIImageView *itemView = [self.saveBannerCustomViews objectSafeAtIndex:index];
        if (!itemView) {
            itemView= [[UIImageView alloc] initWithFrame:CGRectMake(0, 0, kSCREEN_WIDTH, 180)];
            itemView.backgroundColor = [UIColor orangeColor];
            [self.saveBannerCustomViews addObject:itemView];
        }

        if (index % 2 == 0) {
            itemView.frame = CGRectMake(0, -40, kSCREEN_WIDTH, 220);
            itemView.backgroundColor = [UIColor redColor];
        }

        NSString *imgPath = [self.viewModel.customBannerViewImages objectAtIndex:index];

        [itemView sd_setImageWithURL:[NSURL URLWithString:imgPath] placeholderImage:[UIImage imageNamed:@"placeholder"]];

        return itemView;
    }

    return nil;
}
```

## 效果

![](https://ws3.sinaimg.cn/large/006tKfTcly1fk1lcagzrlj30c20nydnn.jpg)


## License

This code is distributed under the terms and conditions of the [MIT license](LICENSE).

## Change-log

A brief summary of each YJBannerView release can be found in the [CHANGELOG](CHANGELOG.mdown).
