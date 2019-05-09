
```python
def test_regular_mocks(mocker):

    input_data = [
        "header1,header2,",
        "some,values",
        "go,here",
        "for,testing"
    ]

    mock_input = mocker.MagicMock(name='in')
    mock_input.return_value.__enter__ = mock_input
    mock_input.return_value.__exit__ = mocker.Mock(return_value=None)
    mock_input.return_value.__iter__.return_value = input_data

    mock_dest = mocker.MagicMock(name='out')

    mock_open = mocker.patch('__builtin__.open')
    # mock_open.return_value = mock_input.return_value

    def get_file(fp, _):
        if fp == 'in':
            return mock_input.return_value
        elif fp == 'out':
            return mock_dest.return_value
        else:
            return mocker.mock_open
    mock_open.side_effect = get_file

    # assert open_and_iter_file('in', 'out')


def test_mock_open(mocker):

    input_data = [
        "header1,header2,",
        "some,values",
        "go,here",
        "for,testing"
    ]

    mock_input = mocker.mock_open(read_data='\n'.join(input_data))
    mock_input.return_value.__iter__.return_value = input_data
    # mock_input.return_value.__enter__ = mock_input
    # mock_input.return_value.__exit__ = mocker.Mock(return_value=None)
    # mock_input.return_value.__iter__.return_value = input_data

    mock_dest = mocker.mock_open()

    mock_open = mocker.patch('__builtin__.open')
    # mock_open.return_value = mock_input.return_value

    print ''

    def get_file(fp, *args, **kwargs):
        print 'getting: ' + fp
        if fp == 'in':
            return mock_input.return_value
        elif fp == 'out':
            return mock_dest.return_value
        else:
            return mocker.mock_open().return_value
    mock_open.side_effect = get_file

    assert open_and_iter_file('in', 'out')


def open_and_iter_file(in_fp, out_fp):
    from csv import DictReader
    lines = []
    with open(in_fp, 'r') as f:
        print f.read()
        print f.readlines()

        print 'f: {}'.format(f)

        reader = DictReader(f)
        for row in reader:
            print 'row: {}'.format(row)
            lines.append(row)

    with open(out_fp, 'w') as f:
        print 'f: {}'.format(f)
        f.writelines(lines)

    return True
```
