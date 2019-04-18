### to export tables in pdf to excel
```
import pandas as pd
import tabula
from pandas import ExcelWriter

file = "sample_data.pdf"
file_name = raw_input("Enter file name: ")
page_num = raw_input("Enter page number: ")
list_dfs = tabula.read_pdf(file, pages = page_num, multiple_tables = True)
# print type(df) 
# print '\n'
# print df 
# df = df[0]
# print type(df)

# for df in df_list:
    # writer = pd.ExcelWriter(file_name + '.xlsx', engine='xlsxwriter')
    # df.to_excel(writer, sheet_name='Sheet' + )
    # print df, '\n'

def save_xls(list_dfs, file_name):
    with ExcelWriter(file_name+'.xlsx') as writer:
        for n, df in enumerate(list_dfs):
            df.to_excel(writer,'sheet%s' % n)
        writer.save()

save_xls(list_dfs, file_name)
# for i in range(len(df_list)):
#     df = df_list[i]
#     writer = pd.ExcelWriter(file_name + '.xlsx', engine='xlsxwriter')
    # print 'before:', i 
    # df.to_excel(writer, sheet_name='Sheet' + str(i))
    # print 'after', i 
# writer.save()
# Create a Pandas Excel writer using XlsxWriter as the engine.
# writer = pd.ExcelWriter('Chapter1.xlsx', engine='xlsxwriter')

# Write each dataframe to a different worksheet.
# df.to_excel(writer, sheet_name='Sheet1')

# Close the Pandas Excel writer and output the Excel file.
# writer.save()

# library(xlsx)
# file <- paste("page1.xlsx", sep = "")
# write.xlsx(USArrests, file, sheetName = "Sheet1") 
# write.xlsx(USArrests, file, sheetName = "Sheet2", append = TRUE)

# convert PDF into CSV
# tabula.convert_into("sample_data.pdf", "page2.csv", output_format="csv", pages='2')

# tabula.convert_into("sample_data.pdf", file_name, output_format="csv", pages=page_num)
```
