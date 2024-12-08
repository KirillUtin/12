import random
def gen_nums(file, num):
  with open(file, 'w') as f:
    for _ in range(num):
      f.write(str(random.randint(1, 100)) + '\n')
def read_avg(file):

  nums = []
  with open(file, 'r') as f:
    for line in f:
      num = int(line.strip())
      nums.append(num)
      print(num)
  if nums:
    avg = sum(nums) / len(nums)
    print(f"\nСреднее: {avg}")
  else:
    print("Файл пуст.")
def main():
  file = input("Введите имя файла: ")
  num = int(input("Введите количество случайных чисел: "))

  gen_nums(file, num)
  read_avg(file)
if __name__ == "__main__":
  main() 
