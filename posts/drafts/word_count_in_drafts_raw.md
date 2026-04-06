hook: a word can explain many things, especialy a word from a lot of people
new problem link: https://platform.stratascratch.com/coding/9817-find-the-number-of-times-each-word-appears-in-drafts?code_type=1

solusinya adalah:

 with raw as (
SELECT
    LOWER(REGEXP_REPLACE(word, '[^a-zA-Z0-9]', '', 'g')) AS word
    FROM google_file_store,
    UNNEST(STRING_TO_ARRAY(contents, ' ')) AS word)
        
select word, count(*) as occurences
from raw
group by word
order by 2 desc

code breakdown: mulai dengan menghilangkan dan menjadikan semua sting menjadi non kapital dan tanpa tanda baca, kemudian menyebar dengan perintah unnest
setelahnya baru menghitung occurance dari kata tersebut

this pattern tells you: kata apa yang paling banyak disebut, hal ini merupakan data cleaning sederhana untuk mendapat kata yang sering muncul. Dari data ini dapat dibuat menjadi wordcloud juga. 

contohkan wordcloud

key takeways: untuk mengolah string perlu beberapa tahapan seperti menerapkan huruf kecil, tanpa tanda baca
