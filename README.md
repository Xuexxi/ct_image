# Lesson 1
setwd("C:/Users/lizhu/Desktop/Bioinformatics 1/xena")
library('tidyverse')

# 读取数据
counts_1 = read.table(file='TCGA-LIHC.htseq_counts.tsv', sep = '\t', header = TRUE)

# 检查列名中字符位置14-16的内容
table(substr(colnames(counts_1), 14, 16))

# 筛选列名中字符位置14-16为 "01A" 或 "11A" 的列
counts_1 = counts_1[, substr(colnames(counts_1), 14, 16) %in% c("01A", "11A")]
table(substr(colnames(counts_1), 14, 16))

# 截取行名的前15个字符作为新的行名
rownames(counts_1) = substr(rownames(counts_1), 1, 15)

# 对数据进行处理
counts = ceiling(2 * counts_1 - 1)

# 保存处理后的数据
write.table(counts, "counts.txt", sep = "\t", row.names = TRUE, col.names = NA, quote = FALSE)

