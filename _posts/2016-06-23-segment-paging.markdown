---
layout: post
title:  "Different segment and paging"
date:   2016-06-23 +0800
categories: OS
---
Confuse about this address translation for a while write this blog to clarify

#same

1.Segmentation and paging both use virtual address
2.Segmentation and paging use table to map to the physical memory
---

#diff

1.segmentation uses __add__ while paging uses concatenation
2.For segment when stack grows it may be get stack overflow, page can allocate new pages 

---
virtual memory contains stack code and data. For stack it start large address and grows downward.
