# Advanced_PolyN_trimming
After adapter trimming, some reads always contains AAAAAA,AAAAAGAAAAA,AAAGAAAAA, AAAAGAAAACAAAAA, ETC.
my tool can solove it.

期望：解决以下痛点​
​1. **复杂残留场景​：**现有工具（如fastp的-g、cutadapt的--poly-a）主要针对连续polyA，但对间断型（如AACAAAA）、嵌合型（polyA/polyN混合）等复杂模式处理不足。

2.** ​三代测序适配​：**PacBio/Nanopore长读长数据中polyA尾更易断裂且混杂非A碱基，需专门优化（如滑动窗口+熵值分析）。
​
3. **提升生物信息学流程鲁棒性​：**作为独立模块，可与fastp/cutadapt串联使用，形成“通用去接头 → 精细去polyA”的分层清洗流程，尤其适合单细胞RNA-Seq、低频突变检测等对数据纯净度要求高的场景。

​4. **技术差异化创新​：**​动态阈值模型​：根据局部序列复杂度（如N碱基密度）自适应调整切除阈值，避免过度修剪真实序列（如保护TTGCAAAA中的基因区域）。

​5. **白名单保护机制​：**对特定模式（如...GA结尾）选择性保留，减少假阳性修剪。
