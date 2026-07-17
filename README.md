from pathlib import Path

class BinaryReader:

    def __init__(self, file):

        self.data = Path(file).read_bytes()

    def read_u32(self, offset):

        return int.from_bytes(
            self.data[offset:offset+4],
            "little"
        )

    def read_string(self, offset, length):

        raw = self.data[offset:offset+length]

        return raw.split(b"\x00")[0].decode(
            errors="ignore"
        )
