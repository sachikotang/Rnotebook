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

#批量读入

list.files("E:\\test",full.names = TRUE)  #或dir("E:\\test",full.names = TRUE) 
dat <- data.frame()
for (i in 1:length(files_full))
  {dat <- rbind(dat, read.csv(files_full[i]))}

##方法1：批量导入：for循环+读入为列表
#适用：有规律的文件名
datalist<-NULL
for( namenum in 1:44 ){
  filename<-paste0("./ReadData/exportExcel (",namenum,").xlsx")
  datalist[[namenum]] = read_excel(filename,sheet = 1)
}

##方法2：批量导入：for循环+读入为列表
#适用：文件名不规律,同一类型文件在同一文件夹下
filename2<- dir("./ReadData")
datalist<-NULL
for(i in 1:length(filename2)){
  filename3<-paste0("./ReadData/",filename2[i])
  datalist[[i]]=read_excel(filename3)

##方法3：批量导入：for循环+读入为列表
#适用：文件名不规律,多个类型xlsx、txt的数据，在同一文件夹下
filename2<- dir("./ReadData")
filename3<-grep("\\.xlsx",filename2,value=TRUE)
datalist<-NULL
for(i in 1:length(filename3)){
  filename4<-paste0("./ReadData/",filename3[i])
  datalist[[i]]=read_excel(filename4)
}
datalist



















fs = list.files('./176031/',pattern = '^GSM')
samples <- substr(fs,1,10)
folders=list.files('./176031/')
folders
library(Seurat)
setwd("C://Users/bing/Desktop/TCGAPRAD/sigcell2/176031/")
scList = lapply(folders,function(folder){ 
  CreateSeuratObject(counts = read.table(folder), 
                     project = folder,
                     min.cells = 3, min.features = 200)
})
