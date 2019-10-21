# README.MD
作业
项目简介：实现一个文本计数统计程序。能正确统计导入的纯英文txt文本中的字符数，单词数，句子数。
首先在D盘中保存一个date.txt的纯英文文件。
如：
https://github.com/wogaijiaoshaming/README.MD/blob/master/photo.png
C语言代码如下：
#include<stdio.h>
#include<stdlib.h>
unsigned long file_size;
unsigned int frequency_count[512];
unsigned int zifu=0,danci=0,juzi=0;
FILE*infilepointer;
void get_frequency_count()
{
	for (unsigned int i=0;i<file_size;i++)
	{
		frequency_count[i]=getc(infilepointer);
	}
	for(unsigned i=0;i<file_size;i++)
    {
        if(frequency_count[i]>='a'&&frequency_count[i]<='z'||frequency_count[i]>='A'&&frequency_count[i]<='Z')
        {
            zifu++;
        }
        if(frequency_count[i]==' '||frequency_count[i]==','||frequency_count[i]=='.'||frequency_count[i]==';'||frequency_count[i]==':'||frequency_count[i]=='?')
        {
            danci++;
        }
        if(frequency_count[i]=='.'||frequency_count[i]=='?')
        {
            juzi++;
        }
    }
 }


bool func(const char*infilename)
{
	if((infilepointer=fopen(infilename,"rb"))!=NULL)
	{
		fseek(infilepointer,0L,2);
		file_size=(unsigned long)ftell(infilepointer);

		fseek(infilepointer,0L,0);
		get_frequency_count();

		fclose(infilepointer);

		return 1;
	}

	else
	{
		printf("Error! can't open %s",infilename);
		return 0;
	}
}
int main()
{
	func("D://date.txt");
    printf("字符个数：%d\n", zifu);
    printf("单词个数：%d\n", danci);
    printf("句子个数：%d\n", juzi);
}
运行结果：
https://github.com/wogaijiaoshaming/README.MD/blob/master/photo2.png
