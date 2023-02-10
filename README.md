# Rnotebook
some notes for R learning
#读大文件
#载入表达矩阵：
exp <- data.table::fread('exp_seq.PRAD-CA.tsv')

#把样品id和患者id串联，组合成新样本名(同一个捐赠者可能存在多个癌或癌旁样品)：
exp2 <- tidyr::unite(exp1, "icgc_specimen_id _ icgc_donor_id", icgc_specimen_id, icgc_donor_id)
colnames(exp2)[1] <- c('sample_id')

##转置
a = read.table("原文件", fill = T, sep = "\t", header = T, stringsAsFactors = FALSE)
b = data.frame(t(a)) #一定是数据框转置,因为输入文件不止一种数据类型
write.table(b,  file = "结果文件", row.names = TRUE, col.names = FALSE, quote = FALSE, sep = "\t")
##或者
fat<-read.table("FATACID.txt",row.names=1,header=F,sep=",")
fat <- t(fat)
fat <- as.data.frame(fat)
