```
if (!is_executable($this->_binary)) {
    throw new Exception(sprintf('wkhtmltopdf binary is not found or not executable: %s', $this->_binary));
}
```