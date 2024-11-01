代码块：

~~~python
def read_daz_file(file_name):  #读
    with open(file_name, 'r' ,encoding='latin1') as file:  
        return file.read() 
  
def decrypt_daz_content(content):  #解密
    hex_values = content.split('X')  
    unicode_chars = [chr(int(hex_val, 16)) for hex_val in hex_values if hex_val]  
    return ''.join(unicode_chars)  
  
def write_to_file(file_name, content, encoding='utf-8'):  #写
    with open(file_name, 'w', encoding=encoding) as file:  
        file.write(content)  
  
def count_visible_characters(text):  #可见字符数
    return sum(1 for char in text if not char.isspace())  
  
def generate_signature(stu_id, total_visible_chars):  #签名
    return f'<解密人>{stu_id}<情报总字数>{total_visible_chars}'  
  
def main():   
    daz_file_name = 'secret.daz'  
    interpretation_file_name = 'interpretation.txt'  
    
    daz_content = read_daz_file(daz_file_name)  
    
    decrypted_content = decrypt_daz_content(daz_content)
    
    write_to_file(interpretation_file_name, decrypted_content)  #明文
    
    with open(interpretation_file_name, 'a', encoding='utf-8') as file:  
        file.write('\n')  
        
    total_visible_chars = count_visible_characters(decrypted_content) 
    
    signature = generate_signature('2024090908007', total_visible_chars)
    
    with open(interpretation_file_name, 'a', encoding='utf-8') as file:  
        file.write(signature)  
~~~

