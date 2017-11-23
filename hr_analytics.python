import numpy
import math

#fileを開いて数値をlistにする
def read_file(input_file):

    file_r = open(input_file, "r")
    lines = file_r.readlines()

    #"YearsWithCurrManager"は各要素に改行が入っているので、改行を削除する
    new_lines = [element.replace("\n","") for element in lines]

    #今のlistの各要素が文字列になっていて、それをlist化にする
    new_list = [element.split(",") for element in new_lines]

    #arrayに変換する
    data_array = numpy.array(new_list)

    #行と列を逆にする
    list_array = data_array.T

    #key = list_array[0][0]
    #value = list_array[0][1:]

    #key = 各要素名, value = 各要素value のdictを作成
    hr_data_dict = {}

    for element in list_array:
        key = element[0]
        hr_data_dict[key] = list(element[1:])

    return hr_data_dict

#計算用のdictに整形する
def data_del(data_dict):

    #valueの形式が数値になっているもののみ残す
    compare_dict = {}

    for key,value in data_dict.items():
        try:
            int_value = [int(e) for e in value]
            compare_dict[key] = int_value
        except ValueError:
            pass

    return compare_dict


#二つのlistを取って、相関係数を返す
def sep_list(list1,list2):

    avgOfList1 = sum(list1)/len(list1)
    avgOfList2 = sum(list2)/len(list2)

    #2つのlistの共分散を求める
    k = 0
    for i in range(len(list1)):
        k = k + (list1[i] - avgOfList1)*(list2[i] - avgOfList2)

    result_k = k/len(list1)

    #2つのlistの標準偏差を求める
    h1 = 0
    for element1 in list1:
        h1 = h1 + (element1 - avgOfList1)*(element1 - avgOfList1)

    result_h1 = math.sqrt(h1/len(list1))

    h2 = 0
    for element2 in list2:
        h2 = h2 + (element2 - avgOfList2)*(element2 - avgOfList2)

    result_h2 = math.sqrt(h2/len(list2))

    if result_k == 0:
        s = 0
    else:
        s = result_k/(result_h1*result_h2)

    return s


#listを指定し、各要素とTWYの相関関数を求める
def cor_result(dict_data, target_key):

    TotalWorkingYears_list = dict_data[target_key]

    cor_dict = {}
    for k,v in dict_data.items():
        if k != target_key:
            cor_dict[k] = sep_list(TotalWorkingYears_list,v)

    return cor_dict


input_file = "hr_raw_data.csv"
data_dict = read_file(input_file)
dict_data = data_del(data_dict)


#maxのkey と valueを返す
def max_cor(cor_dict):

    key_result = max([(v,k) for k,v in cor_dict.items()])[1]

    return key_result

target_key = "EnvironmentSatisfaction"
cor_dict = cor_result(dict_data, target_key)
print(cor_dict)
print(max_cor(cor_dict))


#print(cor_result(list1,list2))
#numpyを使った標準偏差の求め方
#print(numpy.corrcoef(list1, list2)[0, 1])
